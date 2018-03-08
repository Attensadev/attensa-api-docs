# Streams

## Stream Types

Attensa supports the following stream types

Type | Description | Can create | Can search
--------- | ----------- | -------- | ------ | -------
ATTENSA_SEARCH | Composed based on a search of items in other streams in Attensa | Yes | Yes
BING_SEARCH | Bing search results for either web or news search | Yes | Yes
CLINICALTRIALS_SEARCH | Content from clinicaltrials.gov | Yes | Yes
COLLECTION | A combination stream composed of items from other streams | Yes | Yes
FACTIVA_SELECT_HTTP | Content from a Factiva Select feed | No | Yes
PUBMED_SEARCH | Content from PubMed | Yes | Yes
RSS | Content from an RSS feed | Yes | Yes
TWITTER_SEARCH | Content based on a twitter search | Yes | Yes

## GET /streams

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d published=true \
     -d rows=20 \
     -d term=test \
     -d type=COLLECTION \
     https://api.attensa.net/streams
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
    "first": "https://api.attensa.net/streams?rows=20&page=0&term=test&type=COLLECTION&published=true",
    "last": "https://api.attensa.net/streams?rows=20&page=0&term=test&type=COLLECTION&published=true"
  },
  "streams": [{
    "id": "546e17fcd4c67da2547f5b61",
    "title": "Test Stream 01",
    "description": "Description 01",
    "ownerId": "55414a36e4b0436b6280e668",
    "type": "COLLECTION",
    "itemLogoUrl": "https://example.com/path_to_logo/which_will_also_update/items_logo_url.png"
    "emailPostingEnabled": true,
    "openForReading": true,
    "openForPosting": true,
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

Get a paged list of streams.

### Request

`GET https://api.attensa.com/streams`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
published | Filter stream list to published or unpublished streams. Omit for all streams. | No | Boolean | `null`
rows | Number of streams in each page | No | Integer | 20
source.search | Term used for search based stream types (TWITTER_SEARCH, etc) | No | String | `null`
source.uri | Uri of RSS feed for RSS streams | No | String | `null`
term | A search term to narrow the list of streams returned | No | String | `null`
type | Filter results to a specific stream type | No | [searchable stream type](#stream-types) | `null`
tagIds | Filter results to streams with at least one of the tagIds | No | comma separated ID list | `null`
categoryIds | Filter results to streams with at least one of the categoryIds | No | comma separated ID list | `null`

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

## GET /streams/{streamId}

```shell
curl -u username:password https://api.attensa.net/streams/{streamId}
```
> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c67da2547f5b61",
  "title": "Test Stream 01",
  "ownerId": "55414a36e4b0436b6280e668",
  "description" : "Description 01",
  "type": "COLLECTION",
  "itemLogoUrl": "https://example.com/path_to_logo/to_use/to_initialize/items_logoUrl.png",
  "source": {
      "search": "search term",
      "uri": "http://slashdot.org/rss",
      "username": "myUserNameForSecuredRSSFeed"
  },
  "emailPostingEnabled": false,
  "openForReading": true,
  "openForPosting": true,
  "published": true,
  "streamEmailAddress": "test.stream.01@email.attensa.net",
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
  "itemsCount": 0,
  "followersCount": 0,
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
}
```

This endpoint retrieves a specific stream.

### Request

`GET https://api.attensa.net/streams/{streamId}`

### Response

Status code `200`

## GET /streams/{streamId}/items

```shell
curl -u username:password https://api.attensa.net/streams/{streamId}/items
```
> Status code 200 with json structured as follows:

```json
{
  "_links": {
    "first": "https://api.attensa.net/streams/55245b56e4b0db8a310d8767/items?page=0",
    "last": "https://api.attensa.net/streams/55245b56e4b0db8a310d8767/items?page=1",
    "next": "https://api.attensa.net/streams/55245b56e4b0db8a310d8767/items?page=1"
  },
  "_paging": {
    "elementCount": 20,
    "page": 0,
    "pageCount": 2,
    "requestedPageSize": 20,
    "totalElementCount": 34
  },
  "items": [
    {
      "id": "5421214ba4b0fd12d834a223",
      "title": "Lorem Ipsum",
      "shortDescription": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas pulvinar blandit ante vel congue. Nulla et risus interdum, tristique sapien sit amet, suscipit diam. Vestibulum a sem sed lectus sagit",
      "link": "http://www.example.com/lorem/ipsum/2017/05/30",
      "created": "2017-05-30T14:39:18.936Z",
      "modified": "2017-05-30T14:39:18.936Z",
      "published": "2017-05-30T13:30:00.188Z",
      "streamId": "55773111e4b08d8c914d7d1a",
      "streamOriginId": "55773111e4b08d8c914d7d1a",
      "streamOriginTitle": "All the facts in Latin",
      "logoUrl": "https://example.com/initialized_based_on_value_of/stream_item_logo_url.png",
      "commentsCount": 0,
      "likesCount": 0,
      "readersCount": 0,
      "_links": {
        "self": "https://api.attensa.net/items/5421214ba4b0fd12d834a223"
      }
    }
  ]
}
```

Get items for a specific stream.

### Request

`GET https://api.attensa.net/streams/{streamId}/items`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of users in each page | No | Integer | 20
sort | Field to sort the results on | No | attentionaRank, created, modified or published | published
sortDirection | Sort ascending or descending | No | ASC or DESC | DESC
userId | Annotate response with user specific info | No | `null`
includeComments | Field to request comments in response | No | boolean | false
includeFullDescription | Field to request full descriptions | No | boolean | false

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property.
See [GET /items/{itemId}](#get-items-itemid) for an example of the comments json.

<aside class="notice">When the `userId` parameter is used, three properties are added to the normal item objects returned in the `items` array that specify the user's relationship with the item: attentionRank, likedByUser, readByUser and savedByUser.</aside>

## GET /streams/{streamId}/users

```shell
curl -u username:password https://api.attensa.net/streams/{streamId}/users
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
      "_links": {
        "self": "https://api.attensa.net/users/5421903ae4b0fd12d843a219"
      },
      "emailAddress": "test@attensa.com",
      "firstName": "Adam",
      "id": "5421903ae4b0fd12d843a219",
      "lastName": "Test",
      "middleName": "J",
      "status": "ACTIVE",
      "suffix": "SR",
      "timeZone": "US/Pacific",
      "userIsFollowing": false
    }
  ]
}
```

Get users that are following a specific stream.

### Request

`GET https://api.attensa.net/streams/{streamId}/users`

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

## POST /streams

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "title": "Test Stream 01",
       "description": "Description 01",
       "itemLogoUrl": "https://example.com/path_to_logo/to_use/to_initialize/items_logoUrl.png",
       "ownerId": "55414a36e4b0436b6280e668",
       "type": "RSS",
       "source": {
           "uri": "http://slashdot.org/rss",
           "username": "myUserNameForSecuredRSSFeed",
           "password": "myPasswordForSecuredRSSFeed"
       },
       "emailPostingEnabled": false,
       "openForReading": true,
       "rssEnabled": false,
       "tagIds": ["54da78488ab02386a4658eee"],
       "categoryIds" : ["55414a36e4b0436b6280e668"]
     }' \
     https://api.attensa.net/streams
```
> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c67da2547f5b61",
  "title": "Test Stream 01",
  "ownerId": "55414a36e4b0436b6280e668",
  "description" : "Description 01",
  "itemLogoUrl": "https://example.com/path_to_logo/to_use/to_initialize/items_logoUrl.png",
  "type": "RSS",
  "source": {
      "uri": "http://slashdot.org/rss",
      "username": "myUserNameForSecuredRSSFeed"
  },
  "emailPostingEnabled": false,
  "streamEmailAddress": "test.stream.01@email.attensa.net",
  "openForReading": true,
  "openForPosting": true,
  "published": true,
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668"],
  "tagIds": ["54da78488ab02386a4658eee"],
  "itemsCount": 0,
  "followersCount": 0,
  "_links": {
    "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
    "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
  }
}
```

Create a new stream

### Request

`POST https://api.attensa.net/streams`

### JSON request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
title | Stream Title | Yes | String | n/a
description | Stream description | No | String | `null`
ownerId | User id of stream owner | Yes | String of valid user id | n/a
type | Stream type | Yes | [creatable stream type](#stream-types) | n/a
itemLogoUrl | Value used to initialize item.logoUrl | No | String | `null`
source:search | Search term. Only supply for ATTENSA_SEARCH, PUBMED_SEARCH or TWITTER_SEARCH streams | For type ATTENSA_SEARCH, PUBMED_SEARCH, TWITTER_SEARCH | String | `null`
source:uri | Uri of rss feed. Only supply for type RSS streams | For type RSS | String | `null`
source:type | Specify web or news search for BING_SEARCH streams | For type BING_SEARCH | `WEB` or `NEWS` | n/a
source:username | Basic auth username for secured rss feed. Only supply for type RSS streams. | For secured RSS streams | String | `null`
source:password | Basic auth password for secured rss feed. Only supply for type RSS streams. | For secured RSS streams | String | `null`
emailPostingEnabled | Allow posting to COLLECTION stream via email. | No | Boolean | false
streamEmailAddress | Email address to for stream if emailPosting is enabled. Only set for collection streams | No | Valid email string | `null`
openForReading | Allow all users to read this stream | No | boolean | false
openForPosting | Allow all users to post content to a COLLECTION stream | No | boolean | false
published | Publish the stream for users in your account to discover | No | boolean | false
rssEnabled | Allow public access to an RSS feed of this stream | No | boolean | false
tagIds | Stream tag IDs to tag the stream | No | [String] | []
categoryIds | Categories to put the stream in | Yes (empty array for no categories) | [String] | []

<aside class="notice">Including the optional itemLogoUrl will also set the value of the stream's items' logoUrl values in item responses.</aside>

### Response

Status code `201`

## POST /streams/{streamId}/streams

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "streamId": "5519ae56e4b0c0419a88bae1"
     }' \
     https://api.attensa.net/streams/{streamId}/streams
```
> 303 redirect returned pointing to parent stream resource

Add a substream to a COLLECTION stream.

### Request

`POST https://api.attensa.net/streams/{streamId}/streams`

### JSON request body parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
streamId | The streamId of the child stream to be added | Yes | String | n/a

### Response

Status code `303` with `Location` header set to the url of the parent COLLECTION stream

## POST /streams/{streamId}/items

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "author": "John Doe",
       "description": "Description 01",
       "sourceUrl": "http://google.com",
       "title": "Test item 01"
     }' \
     https://api.attensa.net/streams/{streamId}/items
```
> Status code 202 with response as follows:

```json
"Item successfully queued"
```

Post an item to a COLLECTION stream.

### Request

`POST https://api.attensa.net/streams/{streamId}/items`

### JSON request body parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
author | The author name of the item | No | String | `null`
description | The body of the item. | Yes | String | n/a
sourceUrl | Url of the item to link to | No | String | `null`
title | Item title | Yes | String | n/a

### Response

Status code `202`

<aside class="notice">Item creation is asynchronous. While items are typically created whithin a few seconds, there is no guaranteed time frame for when a posted item will be available. </aside>

## POST /streams/{streamId}/items/{itemId}/attachments

```shell
curl -u username:password \
     -H "Content-Type: multipart/form-data" \
     -X POST \
     -F "attachment=@<path_to_target_file>" \
     https://api.attensa.net/streams/{streamId}/items/{itemId}/attachments
```
> Status code 200 with response as follows:

```json
{"result":"Attachment successfully added to Item."}
```

Add a file to an item as an attachment.

### Request

`POST https://api.attensa.net/streams/{streamId}/items/{itemId}/attachments`

### Response

Status code `200`

## PUT /streams/{streamId}

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X PUT \
     -d '{
       "title": "Test Stream 01",
       "description": "Description 01",
       "itemLogoUrl": "https://example.com/path_to_logo/to_use/to_initialize/items_logoUrl.png",
       "ownerId": "55414a36e4b0436b6280e668",
       "source": {
           "uri": "http://slashdot.org/rss",
           "username": "myUserNameForSecuredRSSFeed",
           "password": "myPasswordForSecuredRSSFeed"
       },
       "emailPostingEnabled": false,
       "streamEmailAddress": "test.stream.01@email.attensa.net",
       "openForReading": true,
       "rssEnabled": false,
       "tagIds": ["54da78488ab02386a4658eee"],
       "categoryIds" : ["55414a36e4b0436b6280e668"]
     }' \
     https://api.attensa.net/streams/{streamId}
```
> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c67da2547f5b61",
  "title": "Test Stream 01",
  "ownerId": "55414a36e4b0436b6280e668",
  "description" : "Description 01",
  "itemLogoUrl": "https://example.com/path_to_logo/to_use/to_initialize/items_logoUrl.png",
  "type": "RSS",
  "source": {
      "uri": "http://slashdot.org/rss",
      "username": "myUserNameForSecuredRSSFeed"
  },
  "tagIds": ["54da78488ab02386a4658eee"],
  "emailPostingEnabled": false,
  "openForReading": true,
  "openForPosting": true,
  "published": true,
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668"],
  "itemsCount": 0,
  "followersCount": 0,
  "_links": {
    "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61",
    "owner": "https://api.attensa.net/users/55414a36e4b0436b6280e668"
  }
}
```

Update an existing stream. Updates are applied in a incremental PATCH-like manner, so the entire stream resource does not need to be supplied, only the properties that are changing.

### Request

`PUT https://api.attensa.net/streams/{streamId}`

### JSON body request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
title | Stream Title | No | String | n/a
description | Stream description | No | String | n/a
itemLogoUrl | Value used to initialize item.logoUrl | No | String | `null`
ownerId | User id of stream owner | No | String of valid user id | n/a
source:search | Search term. Only supply for ATTENSA_SEARCH, PUBMED_SEARCH or TWITTER_SEARCH streams | No | String | n/a
source:uri | Uri of rss feed. Only supply for type RSS streams | No | String | n/a
source:username | Basic auth username for secured rss feed. Only supply for type RSS streams. | No | String | n/a
source:password | Basic auth password for secured rss feed. Only supply for type RSS streams. | No | String | n/a
emailPostingEnabled | Allow posting to COLLECTION stream via email. | No | Boolean | n/a
streamEmailAddress | Email address for stream if emailPosting is enabled. Only set for collection streams | No | Valid email string | n/a
openForReading | Allow all users to read this stream | No | Boolean | n/a
openForPosting | Allow all users to post content to a COLLECTION stream | No | Boolean | n/a
published | Publish the stream for users in your account to discover | No | boolean | false
rssEnabled | Allow public access to an RSS feed of this stream | No | Boolean | n/a
tagIds | Stream tag IDs to tag the stream | No | [String] | n/a
categoryIds | Categories to put the stream in | No | [String] | n/a

<aside class="notice">Stream type can not be updated. Once a stream is created it's type is immutable.</aside>
<aside class="notice">All categories or stream tags can be removed by sending an empty categoryIds or tagIds array (<code>"categoryIds": []</code>)</aside>
<aside class="notice">If updating a secured source, all source fields must be sent (uri, username and password). If no username or password is supplied, but a source uri is, then any existing credentials will be removed.</aside>
<aside class="notice">Including the optional itemLogoUrl will also set the value of the stream's items' logoUrl values in item responses.</aside>

### Response

Status code `200`

## DELETE /streams/{streamId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/streams/{streamId}
```
> 204 emtpy body returned on success

Delete an existing stream from the system. All users will be unfollowed from the stream when it is deleted.

<aside class="warning">Use this endpoint with care!  There is no way to undo this action from the API</aside>

### Request

`DELETE https://api.attensa.net/streams/{streamId}`

### Response

Status code `204` with empty body

### Request

`DELETE https://api.attensa.net/streams/{streamId}/streams/{substreamId}`

### Response

Status code `204` with empty body

## DELETE /streams/{streamId}/streams/{substreamId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/streams/{streamId}/streams/{substreamId}
```
> 204 empty body returned on success

Remove a substream from an existing COLLECTION stream.

### Request

`DELETE https://api.attensa.net/streams/{streamId}/streams/{substreamId}`

### Response

Status code `204` with empty body
