## 1. Get categories-

URL - /v1/publisher/categories

Method - GET

E.g.

    curl -H "auth_key: c0c40350-0a16-0130-850c-22000a9d050a"
            "http://api.appsurfer.com/v1/publisher/categories"

Response - 
    
    {
        "categories": [
            {
                "id": 1,
                "name": "Games",
                "type": "MasterCategory"
            },
            {
                "id": 10,
                "name": "Applications",
                "type": "MasterCategory"
            },
            {
                "id": 2,
                "name": "Arcade & Action",
                "type": "SubCategory"
            },
            {
                "id": 3,
                "name": "Brain & Puzzle",
                "type": "SubCategory"
            },
            {
                "id": 4,
                "name": "Cards & Casino",
                "type": "SubCategory"
            },
            {
                "id": 5,
                "name": "Casual",
                "type": "SubCategory"
            },
                    .
                    .
                    .
                    .
                    .
            {
                "id": 36,
                "name": "Other",
                "type": "SubCategory"
            }
        ]
    }
