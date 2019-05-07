# ![LOGO](logo.png) Pims **flow**ground Connector

## Description

A generated **flow**ground connector for the Pims API (version 1.0).

Generated from: https://api.apis.guru/v2/specs/pims.io/1.0/swagger.json<br/>
Generated at: 2019-05-07T17:43:43+03:00

## API Description


Hereafter is the documentation of the private API of [Pims: Pointages Intelligents pour le Monde du Spectacle](https://pims.io). This API is designed for 3rd-party softwares, editors and partners. Its main purpose is to give access the core data of a Pims customer (i.e. events, ticket counts and promotions).

## Authentication
The API uses [basic access authentication](https://en.wikipedia.org/wiki/Basic_access_authentication), meaning you will need a username and password to get authorized.

As each customer in Pims has its own domain (e.g. caramba.pims.io, gdp.pims.io...), each credentials will be valid for one domain/customer only. If you need dedicated credentials for one domain, please contact us. (In any case, we will need an explicit agreement from the customer before we create these credentials.)

<div class="info">
To make your life easy, you can try all endpoints with the public credentials below, pointing to our [demo domain](https://demo.pims.io):
  <ul>
    <li>Base path: `https://demo.pims.io/api`</li>
    <li>Username: `demo`</li>
    <li>Password: `q83792db2GCvgYVdKpU3yG3R`</li>
  </ul>
</div>

## Response format
The API returns JSON and matches the [HAL specification](http://stateless.co/hal_specification.html). The `Content-Type` of each response will be `application/hal+json`, unless an error occurs.

Please note that this documentation describes all responses “as if” they were plain JSON. The specificities of HAL are ignored on purpose, in order to remain compact and avoid repetition.
<div style="-webkit-column-count: 2; -moz-column-count: 2; column-count: 2; -webkit-column-rule: 1px dotted #e0e0e0; -moz-column-rule: 1px dotted #e0e0e0; column-rule: 1px dotted #e0e0e0;">
	<div style="display: inline-block; width:100%;">
		<strong>So when you read in the doc:</strong>
<pre><code class="lang-json">{
	<span class="token string">"id"</span>: <span class="token number">123</span>,
	<span class="token string">"property1"</span>: <span class="token string">"Lorem ipsum"</span>,
	<span class="token string">"object"</span>: {
		<span class="token string">"id"</span>: <span class="token number">456</span>,
		<span class="token string">"property2"</span>: <span class="token number">7.89</span>
	}
}</code></pre>
	</div>
	<div style="display: inline-block; width:100%;">
		<strong>... you'll get in the Real World®:</strong>
<pre><code class="lang-json">{
	<span class="token string">"id"</span>: <span class="token number">123</span>,
	<span class="token string">"property2"</span>: <span class="token string">"Lorem ipsum"</span>,
	<span class="token string">"_embedded"</span>: {
		<span class="token string">"object"</span>: {
			<span class="token string">"id"</span>: <span class="token number">456</span>,
			<span class="token string">"property2"</span>: <span class="token number">7.89</span>,
			<span class="token string">"_links"</span>: {
				<span class="token string">"self"</span>: {
					<span class="token string">"href"</span>: <span class="token string">"https://api.mydomain.com/other-item/456"</span>
				}
			}
		}
	}
	<span class="token string">"_links"</span>: {
		<span class="token string">"self"</span>: {
			<span class="token string">"href"</span>: <span class="token string">"https://api.mydomain.com/item/123"</span>
		}
	}
}</code></pre>
	</div>
</div>

### Errors
Errors return JSON too and tries to match the [Problem Details for HTTP APIs specification](https://tools.ietf.org/html/rfc7807). If it does not match this spec, that's either a bug or a compatibility issue. Please contact us to solve the problem.

The `Content-Type` of errors will be `application/problem+json`. The content will match the following JSON:
```json
{
	"type": "https://tools.ietf.org/html/rfc2616#section-10",
    "title": "Not Found",
	"status": 404,
    "detail": "Entity not found"
}
```

## Versioning
The API is fully versionned, using an URL-versioning scheme: `https://demo.pims.io/api/v1/events`, `https://demo.pims.io/api/v2/events`,...

The version part of the URL is optional, and will be completed with the last stable version if omitted.

## Pagination
All responses corresponding to a collection of resources (e.g. `/venues` or `/series/:id/events`) are paginated. When so, you will only get the first 25 resources you asked for.

If you need to get more resources in one call, you can use the `page_size` query parameter. E.g. `/venues?page_size=50` to get the 50 first venues.

Also note that with HAL, the navigation in paginated responses is a piece of cake, as you can see below:
```json
{
	"_links": {
		"self": {
			"href": "https://demo.pims.io/api/v1/events?page=1"
		},
		"first": {
			"href": "https://demo.pims.io/api/v1/events"
		},
		"last": {
			"href": "https://demo.pims.io/api/v1/events?page=14"
		},
		"next": {
			"href": "https://demo.pims.io/api/v1/events?page=2"
		}
	},
	"_embedded": {
 		... // data content goes here
	},
	"page_count": 14,
	"page_size": 25,
	"total_items": 331,
	"page": 1
}
```

## Filtering and sorting
Every textual filter (e.g. `/events?label=U2`) and/or sort (e.g. `/events?sort=label`) performed with the API uses UTF8_UNICODE_CI collation, meaning it is:
- Case insensitive: “Chloé” will be considered the same as “CHLOÉ”;
- Diacritic insensitive: “Chloé” will be considered the same as “Chloe”.

When performing a sort, it will always be *ascending* by default. To make it *descending*, just use a minus sign (`-`) in front of the parameter value (e.g. `/events?sort=-label`).

## I18n
In responses, some labels can be translated (e.g. promotion types, event input types, etc.). These translatable labels are clearly indicated in the documentation below.

By default, they will be displayed in English, but you can change this behaviour via the `Accept-Language` header. E.g., use `fr` as a value for French.

## PHP SDK
We provide a simple yet convenient SDK for the PHP language, see [the Github page of the project](https://github.com/pimssas/pims-api-client-php).

## And now?
Generaly, you will start by [fetching one or more events](#tag/Events). An <span class="definition">event</span> can be anything that occurs in one venue at one given date and time: a concert, a play, a match, a conference, etc. Additionnally, you can explore the [series](#tag/Series): a <span class="definition">series</span> is just a group of events (e.g. a tour or a festival).

Once you retrieved the events you were interested in, you can look for the sales (<span class="definition">ticket counts</span>):
- Get a quick overview with [`/events/:id/ticket-counts`](#operation/fetchAllTicketCounts)
- Or get a full insight by calling these endpoints:
    1. [`/events/:id/categories`](#operation/fetchAllEventsCategories)
    2. [`/events/:id/channels`](#operation/fetchAllEventsChannels)
    3. [`/events/:id/ticket-counts/detailed`](#operation/fetchAllDetailedTicketCounts)

Eventually, you may also want to fetch the [promotions](#tag/Promotions). A <span class="definition">promotion</span> can be anything meant to leverage the sales: ads, marketing campaigns, buzz or news around the event, etc. A promotion can be linked to any combination of events and/or series.

## Authorization

Supported authorization schemes:
- Basic Authentication

## Actions

### Find all categories

*Tags:* `Categories`

#### Input Parameters
* `label` - _optional_ - Find only the categories whose label/short label contains this value.
* `show_ignored` - _optional_ - If set to `false`, show only the categories which are not ignored. If set to `true`, show all categories.
* `sort` - _optional_ - Sort the categories in the corresponding order.
    Possible values: label, -label, order, -order.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Get one category by ID

*Tags:* `Categories`

#### Input Parameters
* `category_id` - _required_ - ID of the targeted category.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all channels

*Tags:* `Channels`

#### Input Parameters
* `label` - _optional_ - Find only the channels whose label contains this value.
* `show_ignored` - _optional_ - If set to `false`, show only the channels which are not ignored. If set to `true`, show all channels.
* `sort` - _optional_ - Sort the channels in the corresponding order.
    Possible values: label, -label, order, -order.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Get one channel by ID

*Tags:* `Channels`

#### Input Parameters
* `channel_id` - _required_ - ID of the targeted channel.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all events

*Tags:* `Events`

#### Input Parameters
* `label` - _optional_ - Find only the events whose label contains this value.
* `from_datetime` - _optional_ - Find only the events starting after this date.
* `to_datetime` - _optional_ - Find only the events starting before this date.
* `city` - _optional_ - Find only the events whose venue city (or metropolitan area) contains this value.
* `sort` - _optional_ - Sort the events in the corresponding order.
    Possible values: label, -label, datetime, -datetime, venue_label, -venue_label, city, -city.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Get one event by ID

*Tags:* `Events`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all capacities for one event

*Tags:* `Capacities`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `show_ignored` - _optional_ - If set to `false`, show only the [event-]categories which are not ignored. If set to `true`, show everything.
* `sort` - _optional_ - Sort the capacities in the corresponding order.
    Possible values: date, -date.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.

### Get one capacity by ID

*Tags:* `Capacities`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `capacity_id` - _required_ - ID of the targeted capacity.
* `show_ignored` - _optional_ - If set to `false`, show only the [event-]categories which are not ignored. If set to `true`, show everything.

### Find all categories for one event

*Tags:* `Categories`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `show_ignored` - _optional_ - If set to `false`, show only the [event-]categories/[event-]price ranges which are not ignored. If set to `true`, show everything.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.

### Get one event category by ID

*Tags:* `Categories`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `category_id` - _required_ - ID of the targeted event category.
* `show_ignored` - _optional_ - If set to `false`, show only the embedded [event-]price ranges which are not ignored. If set to `true`, show everything.

### Find all channels for one event

*Tags:* `Channels`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `show_ignored` - _optional_ - If set to `false`, show only the [event-]channels which are not ignored. If set to `true`, show everything.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.

### Get one event channel by ID

*Tags:* `Channels`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `channel_id` - _required_ - ID of the targeted event channel.

### Find all promotions for one event

*Tags:* `Promotions`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `label` - _optional_ - Find only the promotions whose label contains this value.
* `from_date` - _optional_ - Find only the promotions starting after this date.
* `to_date` - _optional_ - Find only the promotions ending before this date.
* `type` - _optional_ - Find only the promotions whose type is equal to this value.
* `family` - _optional_ - Find only the promotions whose family is equal to this value.
* `sort` - _optional_ - Sort the promotions in the corresponding order.
    Possible values: date, -date, total_cost, -total_cost.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all ticket counts for one event

*Tags:* `Counts`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `from_date` - _optional_ - Find only the ticket counts after this date.
* `to_date` - _optional_ - Find only the ticket counts before this date.
* `show_ignored` - _optional_ - If set to `false`, show only the [event-]categories/[event-]price ranges/[event]channels which are not ignored. If set to `true`, show everything.
* `show_not_approved` - _optional_ - If set to `false`, show only the approved ticket counts. If set to `true`, show all the ticket counts.
* `sort` - _optional_ - Sort the ticket counts in the corresponding order.
    Possible values: date, -date.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.

### Find all detailed ticket counts for one event

*Tags:* `Counts`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `from_date` - _optional_ - Find only the ticket counts after this date.
* `to_date` - _optional_ - Find only the ticket counts before this date.
* `show_ignored` - _optional_ - If set to `false`, show only the [event-]categories/[event-]price ranges/[event]channels which are not ignored. If set to `true`, show everything.
* `show_not_approved` - _optional_ - If set to `false`, show only the approved ticket counts. If set to `true`, show all the ticket counts.
* `sort` - _optional_ - Sort the ticket counts in the corresponding order.
    Possible values: date, -date.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.

### Get one detailed ticket count by ID

*Tags:* `Counts`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `ticket_count_id` - _required_ - ID of the targeted ticket count.
* `show_ignored` - _optional_ - If set to `false`, show only the [event-]categories/[event-]price ranges/[event]channels which are not ignored. If set to `true`, show everything.

### Get one ticket count by ID

*Tags:* `Counts`

#### Input Parameters
* `event_id` - _required_ - ID of the targeted event.
* `ticket_count_id` - _required_ - ID of the targeted ticket count.
* `show_ignored` - _optional_ - If set to `false`, show only the [event-]categories/[event-]price ranges/[event]channels which are not ignored. If set to `true`, show everything.

### Find all price ranges

*Tags:* `Price ranges`

#### Input Parameters
* `label` - _optional_ - Find only the price ranges whose label contains this value.
* `show_ignored` - _optional_ - If set to `false`, show only the price ranges which are not ignored. If set to `true`, show all price ranges.
* `sort` - _optional_ - Sort the price ranges in the corresponding order.
    Possible values: label, -label, order, -order.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Get one price range by ID

*Tags:* `Price ranges`

#### Input Parameters
* `price_range_id` - _required_ - ID of the targeted price range.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all promotions

*Tags:* `Promotions`

#### Input Parameters
* `label` - _optional_ - Find only the promotions whose label contains this value.
* `from_date` - _optional_ - Find only the promotions starting after this date.
* `to_date` - _optional_ - Find only the promotions ending before this date.
* `type` - _optional_ - Find only the promotions whose type is equal to this value.
* `family` - _optional_ - Find only the promotions whose family is equal to this value.
* `sort` - _optional_ - Sort the promotions in the corresponding order.
    Possible values: date, -date, total_cost, -total_cost.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Get one promotion by ID

*Tags:* `Promotions`

#### Input Parameters
* `promotion_id` - _required_ - ID of the targeted promotion.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all series

*Tags:* `Series`

#### Input Parameters
* `label` - _optional_ - Find only the venues whose label contains this value.
* `from_date` - _optional_ - Find only the series starting after this date.
* `to_date` - _optional_ - Find only the series ending before this date.
* `type` - _optional_ - Find only the series whose type is equal to this value.
    Possible values: TOU, LGS.
* `sort` - _optional_ - Sort the series in the corresponding order.
    Possible values: label, -label, first_date, -first_date, last_date, -last_date.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Get one series by ID

*Tags:* `Series`

#### Input Parameters
* `series_id` - _required_ - ID of the targeted series.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all events for one series

*Tags:* `Events`

#### Input Parameters
* `series_id` - _required_ - ID of the targeted series.
* `from_datetime` - _optional_ - Find only the events starting after this date.
* `to_datetime` - _optional_ - Find only the events starting before this date.
* `city` - _optional_ - Find only the events whose venue city (or metropolitan area) contains this value.
* `sort` - _optional_ - Sort the events in the corresponding order.
    Possible values: label, -label, datetime, -datetime, venue_label, -venue_label, city, -city.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all promotions for one series

*Tags:* `Promotions`

#### Input Parameters
* `series_id` - _required_ - ID of the targeted series.
* `label` - _optional_ - Find only the promotions whose label contains this value.
* `from_date` - _optional_ - Find only the promotions starting after this date.
* `to_date` - _optional_ - Find only the promotions ending before this date.
* `type` - _optional_ - Find only the promotions whose type is equal to this value.
* `family` - _optional_ - Find only the promotions whose family is equal to this value.
* `sort` - _optional_ - Sort the promotions in the corresponding order.
    Possible values: date, -date, total_cost, -total_cost.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all venues

*Tags:* `Venues`

#### Input Parameters
* `label` - _optional_ - Find only the venues whose label contains this value.
* `city` - _optional_ - Find only the venues whose city contains this value.
* `country_code` - _optional_ - Find only the venues whose country_code is equal to this value.
* `type` - _optional_ - Find only the venues whose type is equal to this value.
    Possible values: SAL, FES.
* `sort` - _optional_ - Sort the venues in the corresponding order.
    Possible values: label, -label, city, -city, country, -country.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Get one venue by ID

*Tags:* `Venues`

#### Input Parameters
* `venue_id` - _required_ - ID of the targeted venue.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

### Find all events for one venue

*Tags:* `Events`

#### Input Parameters
* `venue_id` - _required_ - ID of the targeted venue.
* `from_datetime` - _optional_ - Find only the events starting after this date.
* `to_datetime` - _optional_ - Find only the events starting before this date.
* `city` - _optional_ - Find only the events whose venue city (or metropolitan area) contains this value.
* `sort` - _optional_ - Sort the events in the corresponding order.
    Possible values: label, -label, datetime, -datetime, venue_label, -venue_label, city, -city.
* `page_size` - _optional_ - Pagination size, i.e. maximum number of items to be displayed in the response.
* `Accept-Language` - _optional_ - Language used for the translatable labels.
    Possible values: de, en, fr.

## License

**flow**ground :- Telekom iPaaS / pims-io-connector<br/>
Copyright © 2019, [Deutsche Telekom AG](https://www.telekom.de)<br/>
contact: flowground@telekom.de

All files of this connector are licensed under the Apache 2.0 License. For details
see the file LICENSE on the toplevel directory.
