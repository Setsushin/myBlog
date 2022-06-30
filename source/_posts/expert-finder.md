---
title: A SQL "expert finder" function
date: 2021-11-09 20:39:50
categories: Technologies
tags: 
- python
- SQL
---

# Returns a DataFrame with the user IDs who have written Stack Overflow answers on a specific topic.

Inputs:  
topic: A string with the topic of interest  
client: A Client object that specifies the connection to the Stack Overflow dataset  

Outputs:  
results: A DataFrame with columns for _user\_id_ and _number\_of\_answers_.  

```Python
def expert_finder(topic, client):
    my_query = """
               SELECT a.owner_user_id AS user_id, COUNT(1) AS number_of_answers
               FROM `bigquery-public-data.stackoverflow.posts_questions` AS q
               INNER JOIN `bigquery-public-data.stackoverflow.posts_answers` AS a
                   ON q.id = a.parent_Id
               WHERE q.tags like '%{topic}%'
               GROUP BY a.owner_user_id
               ORDER BY number_of_answers DESC
               """

    # Set up the query (a real service would have good error handling for 
    # queries that scan too much data)
    safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)      
    my_query_job = client.query(my_query, job_config=safe_config)

    # API request - run the query, and return a pandas DataFrame
    results = my_query_job.to_dataframe()
    return results
```
    
