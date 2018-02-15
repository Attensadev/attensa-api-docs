# Groups

## GET /groups

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     -d term=test \
     https://api.attensa.net/groups
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
    "first": "https://api.attensa.net/groups?rows=20&page=0&term=test",
    "last": "https://api.attensa.net/groups?rows=20&page=0&term=test"
  },
  "groups": [
    {
      "creatorId": "56161che546097aa51621b47",
      "description": "foo",
      "name": "test",
      "streamCount": 5,
      "userCount": 192,
      "_links": {
          "self": "https://api.attensa.net/groups/55161cf7e4b097aa51621b47"
      }
    }
  ]
}
```

Get a paged list of groups.

### Request

`GET https://api.attensa.net/groups`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of groups in each page | No | Integer | 20
term | A search term to narrow the list of groups returned | No | String | `null`

### Response

Status code `200`

## GET /groups/{groupId}

```shell
curl -u username:password https://api.attensa.net/groups/{groupId}
```
> Status code 200 with response as follows:

```json
{
  "creatorId": "56161che546097aa51621b47",
  "description": "foo",
  "id": "55161cf7e4b097aa51621b47",
  "name": "test",
  "streamCount": 5,
  "userCount": 2,
  "_links": {
    "self": "http://localhost/groups/55161cf7e4b097aa51621b47"
  }
}
```

This endpoint retrieves information about a specific group.

### Request

`GET https://api.attensa.net/groups/{groupsId}`

### Response

Status code `200`

## GET /groups/{groupId}/users

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     -d sort=firstName
     -d sortDirection=ASC
     -d term=test \
     https://api.attensa.net/groups/{groupId}/users
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
    "first": "https://api.attensa.net/groups/{groupId}/users?rows=20&page=0&term=test&sort=firstName&sortDirection=ASC",
    "last": "https://api.attensa.net/groups/{groupId}/users?rows=20&page=0&term=test&sort=firstName&sortDirection=ASC"
  },
  "users": [
    {
      "id": "546e17fcd4c67da2547f5b61",
      "firstName": "test",
      "middleName": "j",
      "lastName": "user",
      "suffix": "sr",
      "emailAddress": "foo@test.com",
      "timeZone": "Europe/Paris",
      "status": "ACTIVE",
      "_links": {
        "self": "https://api.attensa.net/users/546e17fcd4c67da2547f5b61"
      }
    }
  ]
}
```

This endpoint retrieves a paged list of users in a certain group.

### Request

`GET https://api.attensa.com/users`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of users in each page | No | Integer | 20
term | A search term to narrow the list of users returned | No | String | `null`
sort | Field to sort the results on | No | `firstName`, `lastName`, `emailAddress`, `status` | emailAddress
sortDirection | Sort ascending or descending | No | ASC or DESC | ASC

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## GET /groups/{groupId}/streams

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     -d term=test \
     https://api.attensa.net/groups/{groupId}/streams
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
    "first": "https://api.attensa.net/groups/{groupId}/streams?rows=20&page=0&term=test",
    "last": "https://api.attensa.net/groups/{groupId}/streams?rows=20&page=0&term=test"
  },
  "streams": [{
    "title": "Test Stream 01",
    "description": "Description 01",
    "ownerId": "55414a36e4b0436b6280e668",
    "type": "COLLECTION",
    "emailPostingEnabled": true,
    "openForReading": true,
    "openForPosting": true,
    "published": true,
    "streamEmailAddress": "test.stream.01@email.attensa.net",
    "substreams":[
      {
        "id": "559c1972e4b008b9a5329478",
        "title": "Hi, I am a substream!",
        "type": "RSS"
      }
    ],
    "tagIds": ["54da78488ab02386a4658eee"],
    "rssEnabled": false,
    "categoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"]
  }]
}
```

This endpoint retrieves a paged list of streams that a group follows.

### Request

`GET https://api.attensa.com/streams`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of streams in each page | No | Integer | 20
term | A search term to narrow the list of streams returned | No | String | `null`

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## GET /groups/{groupId}/briefings

```shell
curl -u username:password \
     -X GET \
     -d rows=20 \
     -d page=0 \
     https://api.attensa.net/groups/{groupId}/briefings
```

> The above command returns JSON structured like this:

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
    "first": "https://api.attensa.net/groups/{groupId}/briefings?rows=20&page=0",
    "last": "https://api.attensa.net/groups/{groupId}/briefings?rows=20&page=0"
  },
  "briefings": [
    {
      "subject": "My email subject line!",
      "description": "Some special message used by template.",
      "schedule": {
          "startDate": "2015-07-30",
          "stopDate": "2015-08-31",
          "sendHour": "15",
          "sendMinute": "30",
          "frequency": "WEEKLY",
          "interval": 1,
          "sendDays":["MO","TU", "WE", "TH", "FR"],
          "timeZone": "US/Pacific"
      },
      "templateId": "54b58250e4b0ec83add2661e",
      "stream": {
        "catgoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
        "description" : "Description 01",
        "emailPostingEnabled": false,
        "followersCount": 0,
        "id": "546e17fcd4c67da2547f5b61",
        "itemsCount": 0,
        "openForPosting": false,
        "openForReading": true,
        "ownerId": "55414a36e4b0436b6280e668",
        "published": true,
        "rssEnabled": false,
        "source": {
            "uri": "http://slashdot.org/rss"
        },
        "streamEmailAddress": "test.stream.01@email.attensa.net",
        "tagIds": ["54da78488ab02386a4658eee"],
        "title": "Test Stream 01",
        "type": "RSS",
        "_links": {
          "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
          "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
        }
      }
    }
  ]
}
```

This endpoint retrives a list of briefings that a user is subscribed to

### Request

`GET https://api.attensa.com/groups/{groupId}/briefings`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of briefings in each page | No | Integer | 20


### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## POST /groups

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "creatorId": "56161che546097aa51621b47"
       "description": "just a test group",
       "name": "test"
     }' \
     https://api.attensa.net/groups
```
> Status code 201 with response as follows:

```json
{
  "creatorId": "56161che546097aa51621b47",
  "description": "just a test group",
  "id": "55161cf7e4b097aa51621b47",
  "name": "test",
  "streamCount": 0,
  "userCount": 0,
  "_links": {
    "self": "http://localhost/groups/55161cf7e4b097aa51621b47"
  }
}
```

Create a new group.

### Request

`POST https://api.attensa.net/groups`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
creatorId | Id of the user that should be marked as creator | Yes | String | n/a
description | Description of the group | Yes | String | n/a
name | Name of the group | Yes | String | n/a

### Response

Status code `201`

## POST /groups/{groupId}/users

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "id": "56161che546097aa51621b47"
     }' \
     https://api.attensa.net/groups/users
```
> Status code 204 with empty body

Add a user to a group

### Request

`POST https://api.attensa.net/groups/users`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
id | Id of the user that should be added to the group | Yes | String | n/a

### Response

Status code `201`

## POST /groups/{groupId}/streams

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "streamId": "559bf709e4b008a9a53293c3"
     }' \
     https://api.attensa.net/groups/{groupId}/streams
```
> Status code 204 with empty body

Set a group to follow a stream

### Request

`POST https://api.attensa.net/groups/{groupId}/streams`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
streamId | Id of the stream to follow | Yes | String | n/a

### Response

Status code `204`

## PUT /groups/{groupId}

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X PUT \
     -d '{
       "creatorId": "56161che546097aa51621b47"
       "description": "just a test group",
       "name": "test"
     }' \
     https://api.attensa.net/groups/{groupId}
```
> Status code 200 with response as follows:

```json
{
  "creatorId": "56161che546097aa51621b47",
  "description": "just a test group",
  "id": "55161cf7e4b097aa51621b47",
  "name": "test",
  "streamCount": 0,
  "userCount": 0,
  "_links": {
    "self": "http://localhost/groups/55161cf7e4b097aa51621b47"
  }
}
```

Update an existing group. Updates are applied in a incremental PATCH-like manner, so the entire group resource does not need to be supplied, only the properties that are changing.

### Request

`PUT https://api.attensa.net/groups`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
creatorId | Id of the user that should be marked as creator | No | String | n/a
description | Description of the group | No | String | n/a
name | Name of the group | No | String | n/a

### Response

Status code `200`

## DELETE /groups/{groupId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/groups/{groupId}
```
> 204 empty body returned on success

Delete an existing group from the system. All users will be un-followed and un-subscribed from streams they followed or subscribed to via this group.

<aside class="warning">Use this endpoint with care! There is no way to undo this action from the API</aside>

### Request

`DELETE https://api.attensa.net/groups/{groupId}`

### Response

Status code `204` with empty body

## DELETE /groups/{groupId}/users/{userId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/groups/{groupId}/users/{userId}
```
> 204 empty body returned on success

Remove a user from a group.

### Request

`DELETE https://api.attensa.net/groups/{groupId}/users/{userId}`

### Response

Status code `204` with empty body

## DELETE /groups/{groupId}/streams/{streamId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/groups/{groupId}/streams/{streamId}
```
> 204 empty body returned on success

Unfollow a group from a stream.

### Request

`DELETE https://api.attensa.net/groups/{groupId}/streams/{streamId}`

### Response

Status code `204` with empty body.
