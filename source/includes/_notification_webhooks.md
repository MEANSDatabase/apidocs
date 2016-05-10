# Item Posted Notification Webhooks

## When To Use
Subscribe to these webhooks when you have an organization and some users on MEANS and want to be notified when
one of your organization's users is notified of an available item near them.

Examples include:

- An App that helps arrange transportation for your organization

- Claiming items on behalf of your users (when combined with the claiming API method)


## How to Use
Configure your webhook at www.meansdatabase.com/organization. There
you will be able to test that our system can hit your endpoint by sending a test notification to yourself.

> Example using the world's most famous address.

```json
{
"id":"34",
"title":"Fresh Fish",
"user_uuid":32934799208303093,
"posted_at": 13425135235,
"latitude" : -33.863,
"longitude": 151.207,
"full_address":"42 Wallaby Way Sydney NSW 2000 Australia",
"categories": [
  "perishable",
  "protein"
],
"expiration":1461127514,
"donor_will_deliver":false,
"pounds": 56,
"donor_rating": 4.5,
"url":"https://www.meansdatabase.com/items/243235/delicious-fruit"
}
```

Parameter | Type | Description
--------- | ------- | -----------
id | string | The ID of the item posted.
title | string | The title of the item
user_uuid | UUID | The UUID of the user in your organization that is subscribed to this item. This user received either an email or text message.
posted_at | Unix Time | The time the item was posted
latitude | Latitude to 3 decimals | The latitude of the item's location
longitude | Longitude to 3 decimals | The longitude of the item's location
full_address | string | Human-readable representation of the address of the item.
categories | array of strings | List of the categories this item fulfills
expiration | Unix Time | When the post will disappear from MEANS (and possibly the item's food expiration)
donor_will_deliver | boolean | If the donor has offered to deliver the item to this user (user_uuid)
pounds | float to 2 decimals | Representation of the pulling force the earth exhibits on the item
donor_rating | float | Donor's rating as rated by users. 5.0 is perfect, and where everyone starts (but tweaked for notification priority purposes)
url | URL string | The web address of the item, you can direct users to this URL to claim the item.
live | boolean | whether or not this notification is a LIVE or TEST notification.

<aside class="notice">
Our notifier will attempt to notify your endpoint repeatedly using an exponential back-off equation until we get a 200 OK message from your endpoint, so we highly recommend that you include code that makes sure each notification you receive is not a repeat, and that your endpoint returns a 200 response.
</aside>


## Terms
Check Out the Webhooks Terms of Use for a more complete list. We want to encourage food recovery; not bifurcation of information markets. Summary:

- Don't use this to circumvent using MEANS to source food for your organization. We don't charge and we don't enforce exclusivity deals.

- Don't use any part of our API to circumvent limitations imposed by our web interface.

- Don't use the webooks to reverse-engineer our users or donors. You may not use any information received from MEANS for the purposes of building a
food recovery notification platform that competes with MEANS upstream.

- If you want our data, there's a decent chance we build a private API for data-sharing agreements, just ask.
