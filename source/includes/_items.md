# Items

## GET /items

```shell
curl -u username:password https://api.attensa.net/items
```

> The above command returns JSON structured like this:

```json
{
  "_paging": {
    "totalElementCount": 42,
    "pageCount": 3,
    "requestedPageSize": 20,
    "elementCount": 20,
    "page": 0
  },
  "items": [
    {
      "id": "5937ed4ce4b0dde7e4aee583",
      "title": "Lorem Ipsum",
      "shortDescription": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut al",
      "link": "http://www.example.com/lorem/ipsum/2017/05/30",
      "created": "2017-05-30T14:39:18.936Z",
      "modified": "2017-05-30T14:39:18.936Z",
      "published": "2017-05-30T13:30:00.188Z",
      "streamId": "55773111e4b08d8c914d7d1a",
      "streamOriginId": "55773111e4b08d8c914d7d1a",
      "streamOriginTitle": "All the facts in Latin",
      "logoUrl": "https://example.com/set_by_streams/itemLogoUrl.png",
      "commentsCount": 0,
      "likesCount": 0,
      "readersCount": 0,
      "_links": {
        "self": "https://api.attensa.net/items/5937ed4ce4b0dde7e4aee583"
      }
    },
    ...
  ],
  "_links": {
      "first": "https://api.attensa.net/items?page=0",
      "last": "https://api.attensa.net/items?page=2",
      "next": "https://api.attensa.net/items?page=1"
  }
}
```

This endpoint retrieves a paged list of items.

### Request

`GET https://api.attensa.net/items`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of items in each page | No | Integer | 20
sort | Field to sort the results on | No | attentionRank, created, modified or published | published
sortDirection | Sort ascending or descending | No | ASC or DESC | DESC
streamIds | Filter results to streamIds in list | No | comma separated ID list | `null`
userId | Annotate response with user specific info | No | `null`
includeComments | Field to request comments in response | No | boolean | false
includeReadItems | Field to request items read by user | No | boolean | true
includeFullDescription | Field to request full descriptions | No | boolean | false

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property.
See [GET /items/{itemId}](#get-items-itemid) for an example of the comments json.

<aside class="notice">When the `userId` parameter is used, three properties are added to the normal item objects returned in the `items` array that specify the user's relationship with the item: attentionRank, likedByUser, readByUser and savedByUser.</aside>
<aside class="notice">logoUrl is set based on the value of item's stream's itemLogoUrl value.</aside>

## GET /items/{itemId}

```shell
curl -u username:password https://api.attensa.net/items/{itemId}
```

> The above command returns JSON structured like this:

```json
{
  "id": "5937ed4ce4b0dde7e4aee583",
  "title": "Lorem Ipsum",
  "shortDescription": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut al",
  "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
  "logoUrl": "https://example.com/set_by_streams/itemLogoUrl.png",
  "link": "http://www.example.com/lorem/ipsum/2017/05/30",
  "created": "2017-05-30T14:39:18.936Z",
  "modified": "2017-05-30T14:39:18.936Z",
  "published": "2017-05-30T13:30:00.188Z",
  "streamId": "55773111e4b08d8c914d7d1a",
  "streamOriginId": "55773111e4b08d8c914d7d1a",
  "streamOriginTitle": "All the facts in Latin",
  "commentsCount": 0,
  "likesCount": 0,
  "readersCount": 0,
  "comments": [
    {
      "id": "5a944d63e4b09d729edf2fd8",
       "body": "Text body of the comment",
       "created": "2018-01-26T18:09:39.207Z",
       "userId": "54177bb3e4d3fc6238a83bef",
       "userFullName": "Firstname Lastname"
    },
    {
      "id": "5a96c89ee4b075c1b10ac847",
      "body": "Testing adding a comment via customer api",
      "created": "2018-01-28T15:19:58.998Z",
      "userId": "5a173db3d3b0ff0238a83bee",
      "userFullName": "First Last"
    }
  ],
  "_links": {
    "self": "https://api.attensa.net/items/5937ed4ce4b0dde7e4aee583"
  }
}
```

This endpoint retrieves a specific item.

### Request

`GET https://api.attensa.net/items/{itemId}`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
userId | Annotate response with user specific info | No | `null`

### Response

Status code `200`

<aside class="notice">When the `userId` parameter is used, three properties are added to the normal item objects returned in the `items` array that specify the user's relationship with the item: attentionRank, likedByUser, readByUser and savedByUser.</aside>
<aside class="notice">When the `userId` parameter is used, the user will be added to the item's reader list.</aside>
<aside class="notice">logoUrl is set based on the value of item's stream's itemLogoUrl value.</aside>

## POST /items/{itemId}/comments

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "userId": "559bf709e4b008a9a53293c3",
       "body": "Comment text"
     }' \
     https://api.attensa.net/items/{itemId}/comments
```

> The above command returns JSON structured like this:

```json
{
    "id": "5a973318e4b00e62bf99334b",
    "body": "Comment text",
    "created": "2018-01-28T22:54:16.329Z",
    "userId": "559bf709e4b008a9a53293c3",
    "userFullName": "Firstname Lastname"
}
```

This endpoint creates a new user.

### Request

`POST https://api.attensa.net/items/{itemId}/comments`

### JSON request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
userId | Id of the liking user | Yes | String | n/a
body | Comment text | Yes | String | n/a

### Response

Status code `201`

## POST /items/{itemId}/likes

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "userId": "559bf709e4b008a9a53293c3"
     }' \
     https://api.attensa.net/items/{itemId}/likes
```
> Status code 204 with empty body

Set a user to like the item

### Request

`POST https://api.attensa.net/items/{itemId}/likes`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
userId | Id of the liking user | Yes | String | n/a

### Response

Status code `204`

## POST /items/{itemId}/readers

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "userId": "559bf709e4b008a9a53293c3"
     }' \
     https://api.attensa.net/items/{itemId}/readers
```
> Status code 204 with empty body

Add a user to the item's reader list

### Request

`POST https://api.attensa.net/items/{itemId}/readers`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
userId | Id of reading user | Yes | String | n/a

### Response

Status code `204` with empty body

## DELETE /items/{itemId}/comments/{commentId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/items/{itemId}/comments/{commentId}
```
> 204 empty body returned on success

Remove comment from the item.

### Request

`DELETE https://api.attensa.net/items/{itemId}/comments/{commentId}`

### Response

Status code `204` with empty body

## DELETE /items/{itemId}/likes/{userId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/items/{itemId}/likes/{userId}
```
> 204 empty body returned on success

Unset a user from liking the item.

### Request

`DELETE https://api.attensa.net/items/{itemId}/likes/{userId}`

### Response

Status code `204` with empty body

