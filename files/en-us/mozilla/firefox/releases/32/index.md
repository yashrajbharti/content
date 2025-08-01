---
title: Firefox 32 for developers
short-title: Firefox 32
slug: Mozilla/Firefox/Releases/32
page-type: firefox-release-notes
sidebar: firefox
---

Firefox 32 was released on September 2, 2014. This article lists key changes that are useful not only for web developers, but also Firefox and Gecko developers as well as add-on developers.

## Changes for Web developers

### Developer Tools

Highlights:

- [Web Audio Editor](https://firefox-source-docs.mozilla.org/devtools-user/web_audio_editor/index.html)
- _Code completion and inline documentation in Scratchpad]_
- [User agent styles in the Inspector's Rules view](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/index.html#rules-view)
- [Element picker button has moved](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/index.html#firefox-32-onwards-2)
- [Node dimensions added to the Inspector's infobar](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/index.html#firefox-32-onwards)
- [Full page screenshot button added](https://firefox-source-docs.mozilla.org/devtools-user/tools_toolbox/index.html#extra-tools)
- HiDPI images added to the tools
- Nodes that have `display:none` are shown differently in the Inspector

[All devtools bugs fixed between Firefox 31 and Firefox 32](https://bugzilla.mozilla.org/buglist.cgi?resolution=FIXED&classification=Client%20Software&chfieldto=2014-06-09&chfield=resolution&query_format=advanced&chfieldfrom=2014-04-28&chfieldvalue=FIXED&bug_status=RESOLVED&bug_status=VERIFIED&component=Developer%20Tools&component=Developer%20Tools%3A%203D%20View&component=Developer%20Tools%3A%20App%20Manager&component=Developer%20Tools%3A%20Canvas%20Debugger&component=Developer%20Tools%3A%20Console&component=Developer%20Tools%3A%20Debugger&component=Developer%20Tools%3A%20Framework&component=Developer%20Tools%3A%20Graphic%20Commandline%20and%20Toolbar&component=Developer%20Tools%3A%20Inspector&component=Developer%20Tools%3A%20Memory&component=Developer%20Tools%3A%20Netmonitor&component=Developer%20Tools%3A%20Object%20Inspector&component=Developer%20Tools%3A%20Profiler&component=Developer%20Tools%3A%20Responsive%20Mode&component=Developer%20Tools%3A%20Scratchpad&component=Developer%20Tools%3A%20Source%20Editor&component=Developer%20Tools%3A%20Style%20Editor&component=Developer%20Tools%3A%20User%20Stories&component=Developer%20Tools%3A%20WebGL%20Shader%20Editor&product=Firefox).

### CSS

- Enabled {{cssxref("mix-blend-mode")}} by default ([Firefox bug 952643](https://bugzil.la/952643)).
- Enabled `position:sticky` by default in release builds (only enabled on Nightly and Aurora before) ([Firefox bug 916315](https://bugzil.la/916315)).
- Implemented {{cssxref("box-decoration-break")}} and removed the non-standard `-moz-background-inline-policy` ([Firefox bug 613659](https://bugzil.la/613659)).
- Allowed {{cssxref("flex-grow")}} and {{cssxref("flex-shrink")}} to transition between zero and nonzero values, like 'flex-grow: 0.6'([Firefox bug 996945](https://bugzil.la/996945)).

### HTML

- Experimentally implemented, behind a pref, {{HTMLElement("img")}} [`srcset`](/en-US/docs/Web/HTML/Reference/Elements/img#srcset) property, To activate it set `dom.image.srcset.enable` to `true` ([Firefox bug 870021](https://bugzil.la/870021)).
- [**id**](/en-US/docs/Web/HTML/Reference/Global_attributes/id) and [**class**](/en-US/docs/Web/HTML/Reference/Global_attributes/class) are now true [global attributes](/en-US/docs/Web/HTML/Reference/Global_attributes) and also apply to XML elements, in a namespace or not ([Firefox bug 741295](https://bugzil.la/741295)).

### JavaScript

- The following new ECMAScript 2015 built-in methods got implemented:
  - {{jsxref("Array.from()")}} ([Firefox bug 904723](https://bugzil.la/904723)),
  - {{jsxref("Array.prototype.copyWithin()")}} ([Firefox bug 934423](https://bugzil.la/934423)),
  - {{jsxref("Number.isSafeInteger()")}} ([Firefox bug 1003764](https://bugzil.la/1003764)).

### Interfaces/APIs/DOM

- The {{domxref("Navigator.languages")}} property and {{domxref("Window.languagechange_event", "languagechange")}} event have been implemented ([Firefox bug 889335](https://bugzil.la/889335)).
- The {{domxref("Navigator.vibrate()")}} method behavior has been adapted to the latest specification: too long vibrations are now truncated ([Firefox bug 1014581](https://bugzil.la/1014581)).
- The {{domxref("KeyboardEvent.getModifierState()")}} and {{domxref("MouseEvent.getModifierState()")}} methods have been extended to support the `Accel` virtual modifier ([Firefox bug 1009388](https://bugzil.la/1009388)).
- The {{domxref("KeyboardEvent.code")}} property have been experimentally implemented: it is disabled on release build ([Firefox bug 865649](https://bugzil.la/865649)).
- Scoped selectors for {{domxref("Document.querySelector()")}} and {{domxref("Document.querySelectorAll()")}}, for example `querySelector(":scope > li")` have been implemented ([Firefox bug 528456](https://bugzil.la/528456)).
- The experimental implementation of the {{domxref("Document.timeline")}} interface, related to the [Web Animation API](https://drafts.fxtf.org/web-animations/), has been added ([Firefox bug 998246](https://bugzil.la/998246)). It is controlled by `layout.web-animations.api.enabled` preference, enabled only on Nightly and Aurora for the moment.
- The [Data Store API](https://web.archive.org/web/20210613234447/https://developer.mozilla.org/en-US/docs/Archive/B2G_OS/API/Data_Store_API) has been made available to [Web Workers](/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) ([Firefox bug 949325](https://bugzil.la/949325)). It still is only activated for certified applications.
- The [ServiceWorker](/en-US/docs/Web/API/Service_Worker_API) `InstallPhaseEvent` and {{domxref("InstallEvent")}} interfaces have been implemented ([Firefox bug 967264](https://bugzil.la/967264)).
- The MSISDN Verification API, only activated for privileged apps, has been added ([Firefox bug 988469](https://bugzil.la/988469)).
- The [Gamepad API](/en-US/docs/Web/API/Gamepad_API) is now supported on Firefox for Android ([Firefox bug 852935](https://bugzil.la/852935)).
- To match the spec and the evolution of the CSS syntax, minor changes have been done to {{domxref("CSS.escape_static", "CSS.escape()")}}. The identifier now can begins with `'--'` and the second dash must not be escaped. Also vendor identifier are no more escaped. ([Firefox bug 1008719](https://bugzil.la/1008719))
- To complete our Hit Regions implementation, `MouseEvent.region` has been implemented ([Firefox bug 979692](https://bugzil.la/979692)).
- The {{domxref("CanvasRenderingContext2D.drawFocusIfNeeded()")}} method is now enabled by default ([Firefox bug 1004579](https://bugzil.la/1004579)).
- The {{domxref("Navigator.doNotTrack")}} properties now returns `'1'` or `'0'`, reflecting the HTTP value, instead of `'yes'` or `'no'` ([Firefox bug 887703](https://bugzil.la/887703)).
- [XMLHttpRequest.responseURL](/en-US/docs/Web/API/XMLHttpRequest/responseURL) was implemented ([Firefox bug 998076](https://bugzil.la/998076)).

### MathML

- Add support for the {{MathMLElement("menclose")}} notation `phasorangle`.

### SVG

_No change._

### WebRTC

- New constraints for [WebRTC](/en-US/docs/Glossary/WebRTC)'s {{domxref("Navigator.getUserMedia", "getUserMedia()")}}, `width`, `height`, and `framerate`, have been added, to limit stream dimensions and frame rate ([Firefox bug 907352](https://bugzil.la/907352)):

  ```js
  const constraints = {
    mandatory: {
      width: { min: 640 },
      height: { min: 480 },
    },
    optional: [
      { width: 650 },
      { width: { min: 650 } },
      { frameRate: 60 },
      { width: { max: 800 } },
    ],
  };
  ```

- WebRTC methods which previously used callback functions as input parameters are now also available using JavaScript [promises](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

### Audio/Video

_No change._

## Security

- [Privileged code now gets Xray vision for JavaScript `Object` and `Array` instances](https://firefox-source-docs.mozilla.org/dom/scriptSecurity/xray_vision.html#xray-semantics-for-object-and-array).

## Changes for add-on and Mozilla developers

Xray vision is now applied to JavaScript objects that are not themselves DOM objects: [Xrays for JavaScript objects](https://firefox-source-docs.mozilla.org/dom/scriptSecurity/xray_vision.html#xrays-for-javascript-objects).

A `getDataDirectory()` method has been added to `Addon` instances. This method returns the preferred location, within the current profile, for add-ons to store data.

### Add-on SDK

#### Highlights

- Added [`exclude`](https://web.archive.org/web/20210216122834/https://developer.mozilla.org/en-US/docs/Archive/Add-ons/Add-on_SDK/High-Level_APIs/page-mod#pagemod%28options%29) option to `PageMod`.
- Added [`anonymous`](https://web.archive.org/web/20201201022954/https://developer.mozilla.org/en-US/docs/Archive/Add-ons/Add-on_SDK/High-Level_APIs/request#request%28options%29) option to `Request`.
- [Add-on Debugger](https://extensionworkshop.com/documentation/develop/debugging/) now includes a Console and a Scratchpad.

#### Details

[GitHub commits made between Firefox 31 and Firefox 32](https://github.com/mozilla/addon-sdk/compare/firefox31...firefox32). This will not include any uplifts made after this release entered Aurora.

[Bugs fixed between Firefox 31 and Firefox 32](https://bugzilla.mozilla.org/buglist.cgi?resolution=FIXED&chfieldto=2014-06-09&chfield=resolution&query_format=advanced&chfieldfrom=2014-04-28&chfieldvalue=FIXED&bug_status=RESOLVED&bug_status=VERIFIED&bug_status=CLOSED&product=Add-on%20SDK&list_id=10493962). This will not include any uplifts made after this release entered Aurora.

### XPCOM

- The `nsIUDPSocket` interface now provides multicast support through the addition of the new `nsIUDPSocket.multicastLoopback`, `nsIUDPSocket.multicastInterface`, and `nsIUDPSocket.multicastInterfaceAddr` attributes, as well as the `nsIUDPSocket.joinMulticast()` and `nsIUDPSocket.leaveMulticast()` methods.
