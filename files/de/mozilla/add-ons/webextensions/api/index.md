---
title: JavaScript APIs
slug: Mozilla/Add-ons/WebExtensions/API
tags:
  - NeedsTranslation
  - TopicStub
  - WebExtensions
translation_of: Mozilla/Add-ons/WebExtensions/API
---
{{AddonSidebar}}

JavaScript APIs for WebExtensions can be used inside the extension's [background scripts](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Anatomy_of_a_WebExtension#Background_scripts) and in any other documents bundled with the extension, including [browser action](/de/docs/Mozilla/Add-ons/WebExtensions/Browser_action) or [page action](/de/docs/Mozilla/Add-ons/WebExtensions/Page_actions) popups, [sidebars](/de/docs/Mozilla/Add-ons/WebExtensions/Sidebars), [options pages](/de/docs/Mozilla/Add-ons/WebExtensions/Options_pages), or [new tab pages](/en-US/Add-ons/WebExtensions/manifest.json/chrome_url_overrides). A few of these APIs can also be accessed by an extension's [content scripts](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Anatomy_of_a_WebExtension#Content_scripts) (see the [list in the content script guide](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Content_scripts#WebExtension_APIs)).

To use the more powerful APIs you need to [request permission](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/manifest.json/permissions) in your extension's manifest.json.

You can access the APIs using the `browser` namespace:

```js
function logTabs(tabs) {
  console.log(tabs);
}

browser.tabs.query({currentWindow: true}, logTabs);
```

Many of the APIs are asynchronous, returning a [`Promise`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise):

```js
function logCookie(c) {
  console.log(c);
}

function logError(e) {
  console.error(e);
}

var setCookie = browser.cookies.set(
  {url: "https://developer.mozilla.org/"}
);
setCookie.then(logCookie, logError);
```

Note that this is different from Google Chrome's extension system, which uses the `chrome` namespace instead of `browser`, and which uses callbacks instead of promises for asynchronous functions. As a porting aid, the Firefox implementation of WebExtensions APIs supports `chrome` and callbacks as well as `browser` and promises. Mozilla has also written a polyfill which enables code that uses `browser` and promises to work unchanged in Chrome: <https://github.com/mozilla/webextension-polyfill>.

Microsoft Edge uses the `browser` namespace, but doesn't yet support promise-based asynchronous APIs. In Edge, for the time being, asynchronous APIs must use callbacks.

Not all browsers support all the APIs: for the details, see [Browser support for JavaScript APIs](/de/docs/Mozilla/Add-ons/WebExtensions/Browser_support_for_JavaScript_APIs).

{{SubpagesWithSummaries}}
