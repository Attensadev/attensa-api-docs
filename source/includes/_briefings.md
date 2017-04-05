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
      "id": "546e17fcd4c67da2547f5b61",
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

## GET /briefings/{briefingId}/streams

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d rows=20 \
     https://api.attensa.net/briefings/{briefingId}/streams
```

> Status code 200 with response as follows:

```json
{
  "_paging": {
    "totalElementCount": 1,
    "pageCount": 1,
    "requestedPageSize": 20,
    "elementCount": 1,
    "page": 0
  },
  "_links": {
    "first": "https://api.attensa.net/briefings/{briefingId}/streams?page=0&rows=20",
    "last": "https://api.attensa.net/briefings/{briefingId}/streams?page=0&page=20"
  },
  "streams": [{
    "id": "546e17fcd4c67da2547f5b61",
    "title": "Test Stream 01",
    "groupIsSubscribed": true,
    "description": "Description 01",
    "ownerId": "55414a36e4b0436b6280e668",
    "type": "COLLECTION",
    "emailPostingEnabled": true,
    "openForReading": true,
    "openForPosting": false,
    "published": true,
    "streamEmailAddress": "test.stream.01@email.attensa.net",
    "rssEnabled": false,
    "categoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
    "tagIds": ["54da78488ab02386a4658eee"],
    "substreams": [
      {
          "id": "559c1972e4b008b9a5329478",
          "title": "Hi, I am a substream!",
          "type": "RSS"
      }
    ],
    "_links": {
      "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
      "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
    }
  }]
}
```

Get a paged list of streams in the briefing.

### Request

`GET https://api.attensa.com/briefings/{briefingId}/streams`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of streams in each page | No | Integer | 20

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## GET /briefings/{briefingId}/users

```shell
curl -u username:password https://api.attensa.net/briefings/{briefingId}/users
```
> Status code 200 with json structured as follows:

```json
{
  "_links": {
    "first": "https://api.attensa.net/streams/55245b56e4b0db8a310d8767/users?page=0",
    "last": "https://api.attensa.net/streams/55245b56e4b0db8a310d8767/users?page=1",
    "next": "https://api.attensa.net/streams/55245b56e4b0db8a310d8767/users?page=1"
  },
  "_paging": {
    "elementCount": 20,
    "page": 0,
    "pageCount": 2,
    "requestedPageSize": 20,
    "totalElementCount": 34
  },
  "users": [
    {
      "id": "5421903ae4b0fd12d843a219",
      "emailAddress": "test@attensa.com",
      "firstName": "Adam",
      "middleName": "J",
      "lastName": "Test",
      "suffix": "SR",
      "status": "ACTIVE",
      "timeZone": "US/Pacific",
      "_links": {
        "self": "https://api.attensa.net/users/5421903ae4b0fd12d843a219"
      }
    },
    ...
  ]
}
```

Get users that are subscribed to a specific briefing.

### Request

`GET https://api.attensa.net/briefings/{briefingId}/users`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of users in each page | No | Integer | 20
term | A search term to narrow the list of users returned | No | String | `null`
sort | Field to sort the results on | No | firstName, lastName or emailAddress | emailAddress
sortDirection | Sort ascending or descending | No | ASC or DESC | ASC

### Response

Status code `200`

## POST /briefings

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "briefingTitle": "Briefing created via API",
       "templateTitle": "Special per briefing message!",
       "subject": "Your Daily Briefing",
       "description": "A briefing providing daily news updates.",
       "ownerId": "577699bae4b0caf6efc3fdfc",
       "schedule": {
           "startDate": "2017-04-13",
           "sendHour": 10,
           "sendMinute": 30,
           "frequency": "DAILY",
           "timeZone": "US/Pacific"
    },
    "templateId": "54b58250e4b0ec83add2661e",
    "streamIds": ["546e17fcd4c67da2547f5b61", "585206dbe4b06537eec79b04"]
}' \
     https://api.attensa.net/briefings
```
> The above command returns JSON structured like this:

```json
{
  "id": "586ee582e4b05458263553cf",
  "briefingTitle": "Briefing created via API",
  "templateTitle": "Special per briefing message!",
  "subject": "Your Daily Briefing",
  "description": "A briefing providing daily news updates.",
  "ownerId": "577699bae4b0caf6efc3fdfc",
  "templateId": "54b58250e4b0ec83add2661e",
  "subscribersCount": 0,
  "streams": [
    {
      "id": "546e17fcd4c67da2547f5b61",
      "categoryIds": [
        "54c67d6ee4b07a480d551f5c"
      ],
      "emailPostingEnabled": false,
      "followersCount": 1,
      "itemsCount": 373,
      "openForPosting": false,
      "openForReading": true,
      "ownerId": "55414a36e4b0436b6280e668",
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
  "schedule": {
    "startDate": "2017-04-13",
    "sendHour": 10,
    "sendMinute": 30,
    "interval": 1,
    "frequency": "DAILY",
    "timeZone": "US/Pacific"
  },
  "_links": {
    "self": "https://api.attensa.net/briefings/586ee582e4b05458263553cf",
    "owner": "https://api.attensa.net/users/577699bae4b0caf6efc3fdfc"
  }
}
```

Create a new briefing.

### Request

`POST https://api.attensa.net/briefings`

### JSON request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
briefingTitle | Briefing Title | Yes | String | n/a
templateTitle | Custome string for use in templates. | No | String | `null`
description | Long description of the briefing | No | String | `null`
ownerId | User id of briefing owner | Yes | String of valid user id | n/a
subject | Subject line used for sending briefing email | Yes | String | n/a
templateId | Email template to use | No | String of valid template id | id of default template
streamIds | Stream IDs to include in the briefing | No | [String] | []
schedule:startDate | Day to start sending the briefing | Yes | `YYYY-MM-DD` | n/a
schedule:stopDate | Day to stop sending the briefing. Omit to never stop. | No | `YYYY-MM-DD` | `null`
schedule:sendHour | Hour of day to send briefing | Yes | Integer `0-23` | n/a
schedule:sendMinute | Minute of hour to send briefing | Yes | Integer `0-59` | n/a
schedule:frequency | Frequency to send briefing | Yes | `DAILY`, `WEEKLY`, `MONTHLY` | n/a
schedule:interval | Interval of frequency to send.  e.g. send every `<interval>` days  | No | Integer `1-31` | 1
schedule:sendDays | Array of days of the week to send briefing on | For WEEKLY frequency | [`SU`,`MO`,`TU`,`WE`,`TH`,`FR`,`SA`] | n/a
schedule:timeZone | Timezone of requested send time | Yes | [Supported time zone string](#time-zones) | `null`

### Response

Status code `201`

## PUT /briefings/{briefingId}

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X PUT \
     -d '{
       "briefingTitle": "Updated Briefing Example",
       "templateTitle": "New special per briefing message!",
       "subject": "Your Daily Updated Briefing",
       "description": "An updatged briefing providing daily news updates.",
       "ownerId": "577699bae4b0caf6efc3fdfc",
       "schedule": {
           "sendHour": 11,
           "sendMinute": 30,
           "frequency": "WEEKLY",
           "sendDays":["MO", "WE", "FR"],
           "timeZone": "US/Pacific"
    },
    "templateId": "54eba226e4b050dd8b9c1099",
    "streamIds": ["546e17fcd4c67ef6622d3b22"]
}' \
     https://api.attensa.net/briefings/{briefingId}
```
> The above command returns JSON structured like this:

```json
{
  "id": "586ee582e4b05458263553cf",
  "briefingTitle": "Updated Briefing Example",
  "templateTitle": "New special per briefing message!",
  "subject": "Your Daily Updated Briefing",
  "description": "An updatged briefing providing daily news updates.",
  "ownerId": "577699bae4b0caf6efc3fdfc",
  "templateId": "54eba226e4b050dd8b9c1099",
  "subscribersCount": 0,
  "streams": [
    {
      "id": "546e17fcd4c67ef6622d3b22",
      "title": "Example Stream",
      "categoryIds": [
        "54c67d6ee4b07a480d551f5c"
      ],
      "emailPostingEnabled": false,
      "followersCount": 14,
      "itemsCount": 61,
      "openForPosting": false,
      "openForReading": true,
      "ownerId": "55414a36e4b0436b6280e668",
      "published": true,
      "rssEnabled": false,
      "tagIds": ["example"],
      "type": "RSS",
      "substreams": [
        {
          "id": "56d716c0e4b0372417948d9c",
          "title": "New target topic",
          "type": "COLLECTION"
        }
      ],
      "_links": {
        "self": "https://api.attensa.net/streams/546e17fcd4c67ef6622d3b22",
        "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
      },
      "source": {
        "uri": "http://rss.example.com/example"
      }
    }
  ],
  "schedule": {
    "startDate": "2017-04-13",
    "sendHour": 11,
    "sendMinute": 30,
    "interval": 1,
    "frequency": "WEEKLY",
    "sendDays":["MO", "WE", "FR"],
    "interval": 1,
    "timeZone": "US/Pacific"
  },
  "_links": {
    "self": "https://api.attensa.net/briefings/586ee582e4b05458263553cf",
    "owner": "https://api.attensa.net/users/577699bae4b0caf6efc3fdfc"
  }
}
```

Update an existing briefing. Updates are applied in a incremental PATCH-like manner, so the entire briefing resource does not need to be supplied, only the properties that are changing.

### Request

`PUT https://api.attensa.net/briefings/{briefingId}`

### JSON body request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
briefingTitle | Briefing Title | Yes | String | n/a
templateTitle | Custome string for use in templates. | No | String | `null`
description | Long description of the briefing | No | String | `null`
ownerId | User id of briefing owner | Yes | String of valid user id | n/a
subject | Subject line used for sending briefing email | Yes | String | n/a
templateId | Email template to use | No | String of valid template id | id of default template
streamIds | Stream IDs to include in the briefing | No | [String] | []
schedule:startDate | Day to start sending the briefing | Yes | `YYYY-MM-DD` | n/a
schedule:sendHour | Hour of day to send briefing | Yes | Integer `0-23` | n/a
schedule:sendMinute | Minute of hour to send briefing | Yes | Integer `0-59` | n/a
schedule:frequency | Frequency to send briefing | Yes | `DAILY`, `WEEKLY`, `MONTHLY` | n/a
schedule:interval | Interval of frequency to send.  e.g. send every `<interval>` days  | No | Integer `1-31` | 1
schedule:sendDays | Array of days of the week to send briefing on | For WEEKLY frequency | [`SU`,`MO`,`TU`,`WE`,`TH`,`FR`,`SA`] | n/a
schedule:timeZone | Timezone of requested send time | Yes | [Supported time zone string](#time-zones) | `null`

<aside class="notice">All streams can be removed by sending an empty streamIds array (<code>"streamIds": []</code>)</aside>

### Response

Status code `200`

## DELETE /briefings/{briefingId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/briefings/{briefingId}
```
> 204 empty body returned on success

Delete an existing briefing from the system. All users will be unsubscribed from the briefing when it is deleted.

<aside class="warning">Use this endpoint with care! There is no way to undo this action from the API.</aside>

### Request

`DELETE https://api.attensa.net/briefings/{briefingId}`

### Response

Status code `204` with empty body

## DELETE /briefings/{briefingId}/streams/{streamId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/briefings/{briefingId}/streams/{streamId}
```
> 204 empty body returned on success

Remove a stream from a briefing.

### Request

`DELETE https://api.attensa.net/briefings/{briefingId}/streams/{streamId}`

### Response

Status code `204` with empty body

## DELETE /briefings/{briefingId}/users/{userId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/briefings/{briefingId}/users/{userId}
```
> 204 empty body returned on success

Unsubscribe a user from a briefing.

### Request

`DELETE https://api.attensa.net/briefings/{briefingId}/users/{userId}`

### Response

Status code `204` with empty body
