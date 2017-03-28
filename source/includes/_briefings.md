# Briefings

## GET /briefings

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d rows=20 \
     https://api.attensa.net/briefings
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
  "_links": {
    "first": "https://api.attensa.net/briefings?rows=20&page=0",
    "last": "https://api.attensa.net/briefings?rows=20&page=0"
  },
  "briefings": [
    {
      "id": "546e17fcd4c88ef1547b4f33",
      "ownerId": "55414a36e4b0436b6280e668",
      "briefingTitle": "Daily Briefing Example",
      "templateTitle": "Title that can be used inside Templates via helpers",
      "description": "Daily news sent ever day.",
      "subject": "Your Daily News!",
      "templateId": "54eba226e4b050dd8b9c1099",
      "subscriberCount": 0,
      "schedule": {
        "frequency": "DAILY",
        "interval": 2,
        "sendHour": 10,
        "sendMinute": 30,
        "startDate": "2017-03-29",
        "timeZone": "US/Pacific"
      },
      "streamIds": [
        "55fae1c6e4b0efbbd6062867",
        "585206dbe4b06537eec79b04",
        "55e4e635e4b00de911f2259a"
      ]
    }
  ]
}
```

Get a paged list of all enabled briefings.

### Request

`GET /briefings`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of briefings in each page | No | Integer | 20

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property.


## GET /briefings/{briefingId}

```shell
curl -u username:password https://api.attensa.net/briefings/{briefingId}
```
> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c88ef1547b4f33",
  "ownerId": "55414a36e4b0436b6280e668",
  "briefingTitle": "Daily Briefing Example",
  "templateTitle": "Title that can be used inside Templates via helpers.",
  "description": "Daily news sent ever day.",
  "subject": "Your Daily News!",
  "templateId": "54eba226e4b050dd8b9c1099",
  "subscriberCount": 0,
  "schedule": {
    "frequency": "DAILY",
    "interval": 1,
    "sendHour": 10,
    "sendMinute": 30,
    "startDate": "2017-03-29",
    "timeZone": "US/Pacific"
    },
  "streams": [
    {
      "id": "54b57b0ae4b0ec83add26494",
      "categoryIds": [
        "54c67d6ee4b07a480d551f5c"
      ],
      "emailPostingEnabled": false,
      "followersCount": 1,
      "itemsCount": 373,
      "openForPosting": false,
      "openForReading": true,
      "ownerId": "54172bb3e4b0fc6238a83bdf",
      "published": true,
      "rssEnabled": false,
      "tagIds": [],
      "title": "Test Stream 01",
      "type": "RSS",
      "_links": {
        "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
        "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
      },
      "source": {
        "uri": "http://rss.example.com/example"
      }
    },
    {
      "id": "585206dbe4b06537eec79b04",
      "title": "Test Stream 02",
      "ownerId": "53dfb536e4b05bc54063f5f4",
      "categoryIds": [
        "55c100cce4b019471b4dbfa3"
      ],
      "emailPostingEnabled": false,
      "followersCount": 0,
      "itemsCount": 15296,
      "openForPosting": false,
      "openForReading": true,
      "published": true,
      "rssEnabled": false,
      "substreams": [
        {
          "id": "5568efd9e4b07710a6f08f7d",
          "title": "Example source stream Title",
          "type": "RSS"
        },
        {
          "id": "559e9e52e4b09bde8ba71aad",
          "title": "Example Topic Title",
          "type": "COLLECTION"
        }
      ],
      "tagIds": ["test"],
      "type": "COLLECTION",
      "_links": {
        "self": "https://api.attensa.net/streams/585206dbe4b06537eec79b04",
        "owner": "https://api.attensa.net/users/53dfb536e4b05bc54063f5f4"
      }
    }
  ],
  "_links": {
    "self": "https://api.attensa.net/briefings/546e17fcd4c88ef1547b4f33",
    "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
  }
}
```

This endpoint retrieves a specific briefing.

### Request

`GET https://api.attensa.net/briefings/{briefingId}`

### Response

Status code `200`

