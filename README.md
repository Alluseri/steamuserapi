# Steam User API
Steam User API mini-documentation.

## Save Community Preferences

**Endpoint:** https://store.steampowered.com/account/savecommunitypreferences

**Content Type:** application/x-www-form-urlencoded; charset=UTF-8

**Required Headers:** Cookie

**Form Data:**
- community_hide_adult_content_violence: 0 to show adult content w/ violence(On page: Blur and warn about content that may contain frequent violence or gore)
- community_hide_adult_content_sex: 0 to show adult content w/ nudity(On page: Blur and warn about content that may contain frequent nudity or sexual content)
- community_text_filter_setting: 1 to filter profanity and slurs; 2 to filter slurs, but not profanity; 3 to disable filtering(On page: Language Preferences) 
- community_text_filter_ignore_friends: 1 to ignore friends in swearing filter(On page: Do not filter text from my Steam Friends)
- sessionid: Session ID, equal to session ID in Cookie.

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
