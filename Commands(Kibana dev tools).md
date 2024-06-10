# create an index named shakespeare
PUT shakespeare
{
    "settings": {
        "number_of_shards": 3,
        "number_of_replicas": 1
    }
}

# create an index named shakespeare with a specific mapping for the data fields:
PUT /shakespeare
{
    "mappings": {
        "properties": {
            "speaker": {
                "type": "text"
            },
            "play_name": {
                "type": "text"
            },
            "line_id": {
                "type": "long"
            },
            "speech_number": {
                "type": "long"
            }
        }
    }
}

# delete index
DELETE /shakespeare

# without giving id will autogenerate the id no
POST /video_search/_doc
{
    "title": "Machine Learning with Python",
    "description": "Learn machine learning with Python in this tutorial.",
    "duration": 450,
    "published_date": "2023-01-03"
}

# this will use "5" as id
POST /video_search/_doc/5
{
    "title": "Machine Learning with Python",
    "description": "Learn machine learning with Python in this tutorial.",
    "duration": 450,
    "published_date": "2023-01-03"
}

# You can either use put or post but in put you have to give the id which in this case is "4" 
PUT /video_search/_doc/4
{
    "title": "Learning Docker",
    "description": "Learn Docker in this tutorial.",
    "duration": 250,
    "published_date": "2023-01-03"
}

# You can update the data by providing the existing Id (you can use put or post both do the same work)
PUT /video_search/_doc/4
{
    "title": "Learning Docker",
    "description": "Learn Docker in this tutorial.",
    "duration": 250,
    "published_date": "2023-01-03"
}

# if you want to update the specific field
POST /video_search/_doc/5
{
    "title": "Machine Learning with Python",
    "description": "Learn machine learning with Python in this tutorial."
}

# The command you've provided uses the _create endpoint to ensure that the document is created only if 
# it does not already exist. This is useful to avoid accidental updates to an existing document. If a document
# with the same ID already exists, the operation will fail with a 409 Conflict error.
PUT /video_search/_create/4
{
    "title": "Learning Docker",
    "description": "Learn Docker in this tutorial.",
    "duration": 250,
    "published_date": "2023-01-03"
}

# basically elastic search will return only 10 datas
GET /shakespeare/_search

# this will give 1000 datas because you mentioned the size
GET /shakespeare/_search
{
    "query": {
        "match_all": {}
    },
    "size": 1000
}

# get by id
GET /shakespeare/_search
{
    "query": {
        "terms": {
            "_id": [
                "4999",
                "2",
                "3"
            ]
        }
    }
}

# search through field
POST shakespeare/_search
{
    "query": {
        "match": {
            "text_entry": "King"
        }
    }
}

# delete all data
POST /shakespeare/_delete_by_query
{
    "query": {
        "match_all": {}
    }
}

# delete by id
DELETE /shakespeare/_doc/1

# delete group of items with their id
POST /shakespeare/_delete_by_query
{
    "query": {
        "terms": {
            "_id": [
                "4999", "6564"
            ]
        }
    }
}

# This query will return the top 10 most common play_name values in your shakespeare index along with their counts, allowing you to # # see which plays are the most frequent in your data.
GET /shakespeare/_search
{
  "aggs": {
    "by_playname": {
      "terms": {
        "field": "play_name",
        "size": 10
      }
    }
  }
}