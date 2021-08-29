# youtube-bells
**Change the bell setting for all your subscribed channels.** I love YouTube, don't get me wrong, but I don't need every subscribed channel in my Notifications – there is a [Subscriptions feed](https://www.youtube.com/feed/subscriptions) for that. That's why I set all bells to `None`, and picked a few channels for which I wanted to keep on receiving notifications. You may want to do it too :wink:

### Steps:
1. Go to: https://www.youtube.com/feed/channels.
2. Scroll all the way down.
3. Run the script below in your console (`Ctrl+Shift+J`/`Cmd+Alt+J`):

```javascript
(()=>{
var bellOption = 3;
/* alternatively you may change the 3 above (which stands for "None") to:
 * 1 for "All"
 * 2 for "Personalized"
 */
 
var i = 0;
document.querySelectorAll("ytd-subscription-notification-toggle-button-renderer a").forEach(el=>{
	i += 10;
	setTimeout((el)=>{
		el.click();
		document.querySelector(`#items > ytd-menu-service-item-renderer:nth-child(${bellOption})`).click();
	}, i, el);
});
})();
```

Yeah, I know – it's a bit tacky... But hey! It did its job straight away with just a few lines of code 🤷🏽‍♂️
