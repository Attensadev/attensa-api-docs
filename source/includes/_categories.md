# Categories

## GET /categories

```shell
curl -u adam:password https://localhost:8000/categories
```

> Status code 200 with response as follows:

```json
[
    {
        "id": "5547ad95d4c6285588f4b23c",
        "title": "Cheese"
    },
    {
        "id": "9090ad95d4c6285588f4b23c",
        "title": "Wiz"
    }
]
```

This endpoint retrieves a list of categories available to categorize streams into

### Request

`GET https://api.attensa.com/categories`

### Response

Status code `200`

## GET /categories/{categoryId}/streams

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d published=true \
     -d rows=20 \
     -d term=javascript \
     -d type=RSS \
     https://api.attensa.net/categories/{categoryId}/streams
```

> Status code 200 with response as follows:

```json
{
  "_paging": {
    "elementCount": 1,
    "page": 0,
    "pageCount": 1,
    "requestedPageSize": 20,
    "totalElementCount": 1
  },
  "streams": [
    {
      "categoryIds": ["54eba224e4b050dd8b9c1096"],
      "description": "Daily Javascript news",
      "emailPostingEnabled": false,
      "id": "5519ae56e4b0c0419a88bae1",
      "followersCount": 0,
      "itemsCount": 111,
      "openForPosting": false,
      "openForReading": true,
      "ownerId": "54da7849e4b02386a4658e5d",
      "rssEnabled": true,
      "source": {
          "uri": "http://feeds.feedburner.com/dailyjs"
      },
      "title": "DailyJS",
      "type": "RSS",
      "_links": {
          "self": "http://localhost:8000/streams/5519ae56e4b0c0419a88bae1"
      }
    }
  ]
}
```

Get a paged list of streams in a category.

### Request

`GET /categories/{categoryId}/streams`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
published | Filter stream list to published or unpublished streams. Omit for all streams. | No | Boolean | `null`
rows | Number of streams in each page | No | Integer | 20
term | A search term to narrow the list of streams returned | No | String | `null`
type | Filter results to a specific stream type | No | `COLLECTION`, `RSS`, `TWITTER`, `XML` | `null`

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## GET /categories/uncategorized/streams

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d published=true \
     -d rows=20 \
     -d term=javascript \
     -d type=RSS \
     https://api.attensa.net/categories/uncategorized/streams
```

> Status code 200 with response as follows:

```json
{
  "_paging": {
    "elementCount": 1,
    "page": 0,
    "pageCount": 1,
    "requestedPageSize": 20,
    "totalElementCount": 1
  },
  "streams": [
    {
      "categoryIds": [],
      "description": "Daily Javascript news",
      "emailPostingEnabled": false,
      "id": "5519ae56e4b0c0419a88bae1",
      "followersCount": 0,
      "itemsCount": 111,
      "openForPosting": false,
      "openForReading": true,
      "ownerId": "54da7849e4b02386a4658e5d",
      "rssEnabled": true,
      "source": {
          "uri": "http://feeds.feedburner.com/dailyjs"
      },
      "title": "DailyJS",
      "type": "RSS",
      "_links": {
          "self": "http://localhost:8000/streams/5519ae56e4b0c0419a88bae1"
      }
    }
  ]
}
```

Get a paged list of uncategorized streams.

### Request

`GET /categories/uncategorized/streams`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
published | Filter stream list to published or unpublished streams. Omit for all streams. | No | Boolean | `null`
rows | Number of streams in each page | No | Integer | 20
term | A search term to narrow the list of streams returned | No | String | `null`
type | Filter results to a specific stream type | No | `COLLECTION`, `RSS`, `TWITTER`, `XML` | `null`

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## GET /categories/{categoryId}/briefings

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d rows=20 \
     https://api.attensa.net/categories/{categoryId}/briefings
```

> Status code 200 with response as follows:

```json
{
  "_paging": {
    "elementCount": 1,
    "page": 0,
    "pageCount": 1,
    "requestedPageSize": 20,
    "totalElementCount": 1
  },
  "briefings": [
    {
      "description": "javascript news",
      "templateId": "54eba226e4b050dd8b9c1099",
      "title": "DailyJS",
      "schedule": {
        "frequency": "DAILY",
        "interval": 2,
        "sendHour": 10,
        "sendMinute": 40,
        "startDate": "2015-08-08",
        "timeZone": "US/Pacific"
      },
      "stream": {
        "categoryIds": ["54eba224e4b050dd8b9c1096"],
        "emailPostingEnabled": false,
        "id": "5519ae56e4b0c0419a88bae1",
        "followersCount": 0,
        "itemsCount": 111,
        "openForPosting": false,
        "openForReading": true,
        "ownerId": "54da7849e4b02386a4658e5d",
        "rssEnabled": true,
        "source": {
            "uri": "http://feeds.feedburner.com/dailyjs"
        },
        "title": "DailyJS",
        "type": "RSS",
        "_links": {
            "self": "http://localhost:8000/streams/5519ae56e4b0c0419a88bae1"
        }
      }
    }
  ]
}
```

Get a paged list of briefings enabled in a category.

### Request

`GET /categories/{categoryId}/briefings`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of streams in each page | No | Integer | 20

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## GET /categories/uncategorized/briefings

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d rows=20 \
     https://api.attensa.net/categories/uncategorized/briefings
```

> Status code 200 with response as follows:

```json
{
  "_paging": {
    "elementCount": 1,
    "page": 0,
    "pageCount": 1,
    "requestedPageSize": 20,
    "totalElementCount": 1
  },
  "briefings": [
    {
      "description": "javascript news",
      "templateId": "54eba226e4b050dd8b9c1099",
      "title": "DailyJS",
      "schedule": {
        "frequency": "DAILY",
        "interval": 2,
        "sendHour": 10,
        "sendMinute": 40,
        "startDate": "2015-08-08",
        "timeZone": "US/Pacific"
      },
      "stream": {
        "categoryIds": ["54eba224e4b050dd8b9c1096"],
        "emailPostingEnabled": false,
        "id": "5519ae56e4b0c0419a88bae1",
        "followersCount": 0,
        "itemsCount": 111,
        "openForPosting": false,
        "openForReading": true,
        "ownerId": "54da7849e4b02386a4658e5d",
        "rssEnabled": true,
        "source": {
            "uri": "http://feeds.feedburner.com/dailyjs"
        },
        "title": "DailyJS",
        "type": "RSS",
        "_links": {
            "self": "http://localhost:8000/streams/5519ae56e4b0c0419a88bae1"
        }
      }
    }
  ]
}
```

Get a paged list of briefings enabled for streams that are uncategorized.

### Request

`GET /categories/uncategorized/briefings`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of streams in each page | No | Integer | 20

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## PUT /categories

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '[
       {
         "id": "5547ad95d4c6285588f4b23c",
         "title": "Cheese",
       },
       {
         "title": "Wiz",
       }
     ]' \
     https://api.attensa.net/streams/{streamId}/items
```

> Status code 200 with response as follows:

```json
[
    {
        "id": "5547ad95d4c6285588f4b23c",
        "title": "Cheese"
    },
    {
        "id": "9090ad95d4c6285588f4b23c",
        "title": "Wiz"
    }
]
```

### Request

`PUT https://api.attensa.net/categories`

This updates the list of categories available to put streams into.

### JSON request body parameters
An array of category objects should be provided. Each category takes the following form:

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
id | Id of existing category to update title | No | String | `null`
title | Title of the category. | Yes | String | n/a

<aside class="notice">Any category without an id is considered to be new, and will be assigned an id in the response. If an existing category (with id) is included with a different title, the category's title will be updated.</aside>
<aside class="warning">Be careful! If an existing category is not included, it is removed and any associated streams will be disassociate from the removed category.</aside>