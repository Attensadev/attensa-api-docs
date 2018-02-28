# Items

## GET /items

```shell
curl -u username:password https://localhost:8000/items
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

`GET https://api.attensa.com/items`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of items in each page | No | Integer | 20
sort | Field to sort the results on | No | created, modified or published | published
sortDirection | Sort ascending or descending | No | ASC or DESC | DESC
streamIds | Filter results to streamIds in list | No | comma separated ID list | `null`
userId | Annotate response with user specific info | No | `null`
includeReadItems | Field to request items read by user | No | boolean | true
includeFullDescription | Field to request full descriptions | No | boolean | false

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property

<aside class="notice">When the `userId` parameter is used, three properties are added to the normal item objects returned in the `items` array that specify the user's relationship with the item: likedByUser, readByUser and savedByUser.</aside>

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
  "_links": {
    "self": "https://api.attensa.net/items/5937ed4ce4b0dde7e4aee583"
  }
}
```

This endpoint retrieves a specific item.

### Request

`GET https://api.attensa.com/items/{itemId}`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
userId | Annotate response with user specific info | No | `null`

### Response

Status code `200`

<aside class="notice">When the `userId` parameter is used, three properties are added to the normal item objects returned in the `items` array that specify the user's relationship with the item: likedByUser, readByUser and savedByUser.</aside>
<aside class="notice">When the `userId` parameter is used, the user will be added to the item's reader list.</aside>
<aside class="notice">logoUrl is set based on the value of item's stream's itemLogoUrl value.</aside>

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

Status code `204`

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

