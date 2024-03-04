# youtube-bells

**Change the bell setting for all of your subscribed channels.** I love YouTube, don't get me wrong, but I don't need every subscribed channel in my Notifications – that's what the [Subscriptions feed](https://www.youtube.com/feed/subscriptions) is for. That's why I set all the bells to `None`, and picked a few channels that I wanted to continue receiving notifications for. You might want to do the same :wink:

### Steps:
1. Go to: https://www.youtube.com/feed/channels.
2. Scroll all the way down.
3. Run the script below in your console (`Ctrl+Shift+J`/`Cmd+Alt+J`):

```javascript
(async () => {

const bellOption = 3;
/* pick one of:
 * 1 for "All"
 * 2 for "Personalized"
 * 3 for "None"
 */

const clickBellOption = () => {
  document.querySelector(`#items > ytd-menu-service-item-renderer:nth-child(${bellOption})`).click();
};

const wait = async (ms) => {
  return new Promise((resolve) => setTimeout(resolve, ms));
}
 
for (const el of document.querySelectorAll("ytd-subscription-notification-toggle-button-renderer a")) {
  el.click();
  await wait(10);
  clickBellOption();
  await wait(500);
}

})();
```

Yeah, I know – it's a bit tacky... But hey! It did its job straight away with just a few lines of code 🤷🏽‍♂️


## Script for removing all videos from Watch Later

In early 2024, I decided to remove everything from my Watch Later list because it had become useless – I couldn't add anything new. Be sure to change the name of the dropdown option you want the script to click on.

```js
(async () => {

const clickOptionInDropdown = () => {
  const options = [...document.querySelectorAll(`#items > ytd-menu-service-item-renderer`)];
  options.find(opt => opt.innerText === 'Usuń z „Do obejrzenia”')?.click();
}

const wait = async (ms) => {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

const entries = [...document.querySelectorAll("ytd-playlist-video-renderer:has(yt-icon-button)")].reverse();
console.log(`Will work on ${entries.length} elements`);
for (const entry of entries) {
  const dropdownButton = entry.querySelector("yt-icon-button");
  entry.scrollIntoView({ behavior: "instant", block: "center" });
  entry.style.background = "#444";
  dropdownButton.click();
  await wait(10);
  clickOptionInDropdown();
  await wait(500);
  if (window.stopInterval) break;
}
console.log("Done");

})();
```
