# Steam User API
Steam User API mini-documentation.

## Save Community Preferences

**Endpoint:** https://store.steampowered.com/account/savecommunitypreferences

**Content Type:** `application/x-www-form-urlencoded; charset=UTF-8`

**Required Headers:** Cookie

**Request Body:**
- community_hide_adult_content_violence: 0 to show adult content w/ violence(On page: Blur and warn about content that may contain frequent violence or gore)
- community_hide_adult_content_sex: 0 to show adult content w/ nudity(On page: Blur and warn about content that may contain frequent nudity or sexual content)
- community_text_filter_setting: 1 to filter profanity and slurs; 2 to filter slurs, but not profanity; 3 to disable filtering(On page: Language Preferences) 
- community_text_filter_ignore_friends: 1 to ignore friends in swearing filter(On page: Do not filter text from my Steam Friends)
- sessionid: Session ID, same as in the Cookie header

**Response:** Coming soon!

**Example Code(Javascript):**
```js
function disableSwearFilter(cookie) {
	fetch("https://store.steampowered.com/account/savecommunitypreferences", {
		method: "POST",
		credentials: 'include',
		headers: {"Content-Type": "application/x-www-form-urlencoded; charset=UTF-8","Cookie":cookie},
		body: ("community_hide_adult_content_violence=0&community_hide_adult_content_sex=0&community_text_filter_setting=3&community_text_filter_ignore_friends=1&sessionid="+cookie.match("sessionid=(.+?);")[1])
	});
}
```

## Edit User Profile
**Endpoint:** https://steamcommunity.com/profiles/{0}/edit/ **where** {0} is your SteamID

**Content Type:** `multipart/form-data; boundary=----WebKitFormBoundaryxVeZNwaTek1hh59r` **where** boundary can be any valid form boundary.

**Required Headers:** Cookie

**Request Body:**

*Notice!* The Content Type of this request is form-data, so the request body must be formed accordingly.

- sessionID: Session ID, same as in the Cookie header
- type: Always profileSave
- weblink\_1\_title: Always empty
- weblink\_1\_url: Always empty
- weblink\_2\_title: Always empty
- weblink\_2\_url: Always empty
- weblink\_3\_title: Always empty
- weblink\_3\_url: Always empty
- personaName: Your profile name(On page: Profile Name)
- real_name: Your real name(On page: Real Name)
- customURL: Your custom profile URL(On page: Custom URL)
- country: Your country's ISO 3166-1 Alpha-2 code(On page: Country)
- state: Your geographic state, equal to statecode in response(See Query Locations, States; On page: State/Province)
- city: Your city, equal to cityid in response(See Query Locations, City; On page: City)
- summary: Your profile description(On page: Summary)
- hide_profile_awards: 1 to hide profile awards(On page: Hide Community Awards on my profile)
- type: Always profileSave(*Notice!* Yes, this entry is indeed appearing twice, it's not an error in this documentation)
- sessionID: Session ID, same as in the Cookie header(*Notice!* Yes, this entry is indeed appearing twice, it's not an error in this documentation)
- json: Always 1

**Response:** Coming soon!

**Example Code:** Coming soon!

## Query Locations
https://steamcommunity.com//actions/QueryLocations/CN/

https://steamcommunity.com//actions/QueryLocations/CN/03

Coming soon.
