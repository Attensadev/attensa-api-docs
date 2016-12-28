# Template Data

## Briefing Variables

Briefing data helpers available to templates.

### `items` > `item` : 

These are all the items in the briefing, with standard item data, plus the following:

* `{{title}}`: The title of the item.
* `{{link}}`: A link to the content of the item in the Attensa reading view.
* `{{sourceLink}}`: A link to the content's original source.
* `{{linkResolverLink}}`: Provides a link resolver link for the article if one exists.
* `{{author}}`: The full name of the author of the item. 
* `{{defaultDescription}}`: The full text of the item description.
* `{{cleanDescription}}`: The same text as defaultDescription with any HTML stripped off.
* `{{shortDescription}}`: The same text as cleanDescription with a limitation to 200 characters.
* `{{publishedDate}}`: The item's published date.


### `briefing` : 

* `{{briefing.briefingTitle}}`: The title text for the briefing.
* `{{briefing.templateTitle}}`: The title text for the briefing's template. 
* `{{briefing.description}}`: The briefing's description.
* `{{viewAsHTML}}`: A link to the HTML version of the briefing inside of Attensa.
* `{{totalNewItems}}`: The count of items added since the last briefing was sent. 
* `{{startDate}}`: The start date and time of the briefing.
* `{{endDate}}`: The end date and time of the briefing.
* `{{recipientUserId}}`: The userId of the recipient of the briefing email.
* `{{hostName}}`: The hostName of the tenancy sending the briefing.
* `{{indexedStreams}}`: The first level of non-empty streams in a briefing, with the following:
* `{{streamId}}`: The indexed stream's Id.
* `{{streamTitle}}`: The indexed stream's title.
* `{{streamDescription}}`: The indexed stream's description.
* `{{itemsCount}}`: Count of items in the indexed stream.
* `{{items}}`: All items in the indexed stream.

## Top level Topic Variables available to Topic Briefings only

Topic data helpers available to Topic Briefings' templates only. Standalone Briefings do not have a top level topic.

### `stream` :

* `{{stream.title}}`: Thop level Topic's title.
* `{{stream.description}}`: The top level Topic's description
* `{{stream.followersCount}}`: The number of followers following that a stream.

### Topic Views for Topic Briefings:

* `{{topicView}}`: A link to the topic view.
* `{{indexedTopicView}}`: A link to the new topic view with the index displayed.
* `{{noNavTopicView}}`: A link to the new topic view with no navigation displayed.
* `{{noNavIndexedTopicView}}`: A link to the new topic view with the index displayed but no navigation displayed.
