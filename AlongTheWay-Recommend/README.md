# AlongTheWay-Recommend
Recommend Point of Interests

## Getting started

- setup AWS account

- serverless

```buildoutcfg
npm install -g serverless
npm update -g serverless
```

more details
https://serverless.com/framework/docs/providers/aws/guide/quick-start/

## Deploying

```buildoutcfg
sls deploy
```

## APIs

### getFirstRandomPOIs

note:
- big_bucket should be either 1 (food-related POI) or 2 (activity-related POI) 

```buildoutcfg
curl -X POST \
https://j51wl2ae9c.execute-api.us-east-1.amazonaws.com/dev/getFirstRandomPOIs \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
  "big_bucket": 1,
  "origin": [34.05223, -118.24368],
  "destination": [37.77493, -122.41942]
}' | jq .
```
 
output: 10 POIs

```buildoutcfg
[
  {
    "id": "4b6b781ff964a520ca0a2ce3",
    "name": "Del Monte Cafe",
    "category": "'café'",
    "image_url": "https://fastly.4sqi.net/img/general/300x500/4032327_-rDxRJKtH8rZc_NMRPlX43LSDWjmtEdivcSYsKV-QMQ.jpg",
    "rating": 8.2,
    "lat": 35.27420654,
    "lng": -120.6563386,
    "city": "San Luis Obispo"
  },
  {
    "id": "53dd9944498e95484c46a480",
    "name": "Old San Luis BBQ Co.",
    "category": "'bbq joint'",
    "image_url": "https://fastly.4sqi.net/img/general/300x500/87664271_MbHUioPNh81lEz2iaJD8RWA-Z27rjIEM5Q2XYULWqfs.jpg",
    "rating": 8.1,
    "lat": 35.27857536,
    "lng": -120.665379,
    "city": "San Luis Obispo"
  },
  {
    "id": "5082fa57e4b0ad74a87e47f4",
    "name": "Chop Street",
    "category": "'salad place'",
    "image_url": "https://fastly.4sqi.net/img/general/300x500/2634741_y-eW9tGGN7zBdtxD2ygJCEz7IVmifJJ8MhMAK2W-8ds.jpg",
    "rating": 7.5,
    "lat": 35.14199045,
    "lng": -120.6405363,
    "city": "Pismo Beach"
  },
  ...
]
```

### getPersonalizedPOIs

note:
- preference should be either 0 (don't like) or 1 (like)

```buildoutcfg
curl -X POST \
https://j51wl2ae9c.execute-api.us-east-1.amazonaws.com/dev/getPersonalizedPOIs \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
  "big_bucket": 1,
  "origin": [34.05223, -118.24368],
  "destination": [37.77493, -122.41942],
  "user_preferences": [
            {"id": "4bafbe03f964a520ec1c3ce3",
             "preference": 0},
            {"id": "426d8480f964a5205f211fe3",
             "preference": 1},
            {"id": "4af49794f964a52027f421e3",
             "preference": 1},
            {"id": "4b71c8eff964a520435c2de3",
             "preference": 0},
            {"id": "4c1c91f8fcf8c9b60b4aaa0b",
             "preference": 1},
            {"id": "50a59ef3e4b07223cec8b49a",
             "preference": 1},
            {"id": "4bcb545a0687ef3b6c7cddcc",
             "preference": 1},
            {"id": "5b1739f0974617002c65a18f",
             "preference": 0},
            {"id": "4b08a15cf964a520db0f23e3",
             "preference": 1},
            {"id": "4c06b8db0e0a2d7fee48ec0c",
             "preference": 1}
        ]
}' | jq .
```

output: 50 POIs

```buildoutcfg
[
  {
    "id": "4b6b781ff964a520ca0a2ce3",
    "name": "Del Monte Cafe",
    "category": "'café'",
    "image_url": "https://fastly.4sqi.net/img/general/300x500/4032327_-rDxRJKtH8rZc_NMRPlX43LSDWjmtEdivcSYsKV-QMQ.jpg",
    "rating": 8.2,
    "lat": 35.27420654,
    "lng": -120.6563386,
    "city": "San Luis Obispo"
  },
  {
    "id": "53dd9944498e95484c46a480",
    "name": "Old San Luis BBQ Co.",
    "category": "'bbq joint'",
    "image_url": "https://fastly.4sqi.net/img/general/300x500/87664271_MbHUioPNh81lEz2iaJD8RWA-Z27rjIEM5Q2XYULWqfs.jpg",
    "rating": 8.1,
    "lat": 35.27857536,
    "lng": -120.665379,
    "city": "San Luis Obispo"
  },
  {
    "id": "5082fa57e4b0ad74a87e47f4",
    "name": "Chop Street",
    "category": "'salad place'",
    "image_url": "https://fastly.4sqi.net/img/general/300x500/2634741_y-eW9tGGN7zBdtxD2ygJCEz7IVmifJJ8MhMAK2W-8ds.jpg",
    "rating": 7.5,
    "lat": 35.14199045,
    "lng": -120.6405363,
    "city": "Pismo Beach"
  },
  ...
]
```