# Steam User API
Steam User API mini-documentation.

## Save Community Preferences

**Endpoint:** POST https://store.steampowered.com/account/savecommunitypreferences

**Content Type:** `application/x-www-form-urlencoded; charset=UTF-8`

**Required Headers:** Cookie

**Request Body:**
- community_hide_adult_content_violence: 0 to show adult content w/ violence(On page: Blur and warn about content that may contain frequent violence or gore)
- community_hide_adult_content_sex: 0 to show adult content w/ nudity(On page: Blur and warn about content that may contain frequent nudity or sexual content)
- community_text_filter_setting: 1 to filter profanity and slurs; 2 to filter slurs, but not profanity; 3 to disable filtering(On page: Language Preferences) 
- community_text_filter_ignore_friends: 1 to ignore friends in swearing filter(On page: Do not filter text from my Steam Friends)
- sessionid: Session ID, same as in the Cookie header

**Success Response:** Exact { "success": 1 }

**Example Usage Code(Javascript):**
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

**Content Type:** `multipart/form-data`

**Required Headers:** Cookie

**Request Body:**

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
- type: **Dupe**
- sessionID: **Dupe**
- json: Always 1

**Success Response:** Exact { "success": 1, "errmsg": "" }

## Query Locations
### States
**Endpoint:** GET https://steamcommunity.com//actions/QueryLocations/{0} **where** {0} is your country's ISO 3166-1 Alpha-2 code.

**Response:** Mappable { "countrycode": string, "statecode": number, "statename": string }

### City
**Endpoint:** GET https://steamcommunity.com//actions/QueryLocations/{0}/{1} **where** {0} is your country's ISO 3166-1 Alpha-2 code, {1} is the statecode of some state in your country

**Response:** Mappable { "countrycode": string, "statecode": number, "cityid": number, "cityname": string }

## Emoticons
**Endpoint:** GET https://steamcommunity.com/actions/EmoticonData

**Required Headers:** Cookie

**Success Response:**
```
Exact {
emoticons: Mappable { 
	"appid": number, // The app this emote comes from's ID, 0 for Steam emotes
	"count": number, // The amount of copies of this emote you have in your inventory, starting from 1
	"name": string, // The emote name, e.g. ":steamthis:", COLONS INCLUDED!
	"time_last_used": null/number, // The time you last used this emote, null if never.
	"time_received": number, // The time you received this emote at. Not null even for Steam emotes.
	"use_count": null/number // How many times you used this emote, null if never.
},
rwgrsn: -2, // May be a different value + unknown usage!
success: 1
}
```

## TODOs
GET https://steamcommunity.com/actions/GetNotificationCounts
GET https://store.steampowered.com/dynamicstore/userdata/?id={0}&cc=RU&v=35
GET https://store.steampowered.com/tagdata/populartags/russian
GET https://api.steampowered.com/IPlayerService/GetProfileItemsOwned/v1?access_token={0}&input_protobuf_encoded={1}
GET https://api.steampowered.com/IPlayerService/GetProfileItemsEquipped/v1?access_token={0}&input_protobuf_encoded={1}
GET https://steamcommunity.com/id/alluseri/ajaxgroupinvite?select_primary=1&json=1

# Defintions
## Exact
An exact representation of a JSON object.

**Example:** `Exact { "success": 1 }` is **exactly** the same as `{"success":1}` in JS and JSON.
## Mappable
An array with every element matching one scheme, making it(the array) mappable.

Important: Mappables are ARRAYS OF OBJECTS, not OBJECTS!

**Example:** `Mappable { "id": number, "name": string }` can be represented as an array with any amount of elements matching the given map, e.g.: `[{"id":1243,"name":"Catgirls"},{"id":45444,"name":"are"},{"id":1337420,"name":"supreme"}]`, which can be mapped using e.g. ``(x)=>{console.log(`${x.id} = ${x.name}`)}``.

# Important remarks
The non-null "string" type CANNOT or IS NOT KNOWN TO EVER be null.
