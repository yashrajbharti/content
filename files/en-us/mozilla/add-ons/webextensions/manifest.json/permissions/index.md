---
title: permissions
slug: Mozilla/Add-ons/WebExtensions/manifest.json/permissions
page-type: webextension-manifest-key
browser-compat: webextensions.manifest.permissions
sidebar: addonsidebar
---

<table class="fullwidth-table standard-table">
  <tbody>
    <tr>
      <th scope="row">Type</th>
      <td><code>Array</code></td>
    </tr>
    <tr>
      <th scope="row">Mandatory</th>
      <td>No</td>
    </tr>
    <tr>
      <th scope="row">Manifest version</th>
      <td>2 or higher</td>
    </tr>
    <tr>
      <th scope="row">Example</th>
      <td>
        <pre class="brush: json">
"permissions": [
  "webRequest"
]</pre
        >
      </td>
    </tr>
  </tbody>
</table>

Use the `permissions` key to request special powers for your extension. This key is an array of strings, and each string is a request for a permission.

If you request permissions using this key, then the browser may inform the user at install time that the extension is requesting certain privileges, and ask them to confirm that they are happy to grant these privileges. The browser may also allow the user to inspect an extension's privileges after installation. As the request to grant privileges may impact on users' willingness to install your extension, requesting privileges is worth careful consideration. For example, you want to avoid requesting unnecessary permissions and may want to provide information about why you are requesting permissions in your extension's store description. More information on the issues you should consider is provided in the article [Request the right permissions](https://extensionworkshop.com/documentation/develop/request-the-right-permissions/).

For information on how to test and preview permission requests, see [Test permission requests](https://extensionworkshop.com/documentation/develop/test-permission-requests/) on the Extension Workshop site.

The key can contain three kinds of permissions:

- host permissions (Manifest V2 only, host permissions are specified in the [`host_permissions`](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/host_permissions) manifest key for Manifest V3 or higher.)
- API permissions
- the `activeTab` permission

## Host permissions

> [!NOTE]
> How you request host permissions depends on whether you want them at install time or runtime and which manifest version your extension is using.
>
> - Manifest V2:
>   - install time request with this (`permissions`) manifest key.
>   - runtime request with the [`optional_permissions`](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/optional_permissions) manifest key.
> - Manifest V3 or higher:
>   - install time request with the [`host_permissions`](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/host_permissions) manifest key.
>   - runtime request with the [`optional_host_permissions`](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/optional_host_permissions) manifest key.

Host permissions are specified as [match patterns](/en-US/docs/Mozilla/Add-ons/WebExtensions/Match_patterns), and each pattern identifies a group of URLs for which the extension is requesting extra privileges. For example, a host permission could be `"*://developer.mozilla.org/*"`.

The extra privileges include:

- [XMLHttpRequest](/en-US/docs/Web/API/XMLHttpRequest) and [fetch](/en-US/docs/Web/API/Fetch_API) access to those origins without cross-origin restrictions (even for requests made from content scripts)
- the ability to read tab-specific metadata without the "tabs" permission, such as the `url`, `title`, and `favIconUrl` properties of {{WebExtAPIRef("tabs.Tab")}} objects
- the ability to [inject content scripts](/en-US/docs/Mozilla/Add-ons/WebExtensions/Content_scripts#loading_content_scripts) and styles programmatically into pages served from those origins.
- the ability to receive events from the {{webextAPIref("webRequest")}} API for these hosts
- the ability to access cookies for that host using the {{webextAPIref("cookies")}} API, as long as the `"cookies"` API permission is also included.
- bypassing tracking protection for extension pages where a host is specified as a full domain or with wildcards. Content scripts, however, can only bypass tracking protection for hosts specified with a full domain.

In Firefox, from version 56 onwards, extensions automatically get host permissions for their own origin, which is of the form:

```url
moz-extension://60a20a9b-1ad4-af49-9b6c-c64c98c37920/
```

where `60a20a9b-1ad4-af49-9b6c-c64c98c37920` is the extension's internal ID. The extension can get this URL programmatically by calling {{webextAPIref("extension/getURL", "extension.getURL()")}}:

```js
browser.extension.getURL("");
// moz-extension://60a20a9b-1ad4-af49-9b6c-c64c98c37920/
```

## API permissions

API permissions are specified as keywords, and each keyword names a [WebExtension API](/en-US/docs/Mozilla/Add-ons/WebExtensions/API) that the extension would like to use.

These permissions are available in Manifest V2 and above unless otherwise noted:

- `activeTab`
- `alarms`
- `background`
- `bookmarks`
- `browserSettings`
- `browsingData`
- `captivePortal`
- `clipboardRead`
- `clipboardWrite`
- `contentSettings`
- `contextMenus`
- `contextualIdentities`
- `cookies`
- `debugger`
- `declarativeNetRequest`
- `declarativeNetRequestFeedback`
- `declarativeNetRequestWithHostAccess`
- `devtools` (This permission is granted implicitly when the [`devtools_page`](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/devtools_page) manifest key is present.)
- `dns`
- `downloads`
- `downloads.open`
- `find`
- `geolocation`
- `history`
- `identity`
- `idle`
- `management`
- `menus`
- `menus.overrideContext`
- `nativeMessaging`
- `notifications`
- `pageCapture`
- `pkcs11`
- `privacy`
- `proxy`
- `scripting`
- `search`
- `sessions`
- `storage`
- `tabGroups`
- `tabHide`
- `tabs`
- `theme`
- `topSites`
- `unlimitedStorage`
- 'userScripts' (see [userScripts permission](/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts#permissions))
- `webNavigation`
- `webRequest`
- `webRequestAuthProvider` (Manifest V3 and above)
- `webRequestBlocking`
- `webRequestFilterResponse`
- `webRequestFilterResponse.serviceWorkerScript`

In most cases the permission just grants access to the API, with the following exceptions:

- `tabs` gives you access to [privileged parts of the `tabs` API](/en-US/docs/Mozilla/Add-ons/WebExtensions/API/tabs) without the need for [host permissions](#host_permissions): `Tab.url`, `Tab.title`, and `Tab.faviconUrl`.
  - In Firefox 85 and earlier, you also need `tabs` if you want to include `url` in the `queryInfo` parameter to {{webextAPIref("tabs/query", "tabs.query()")}}. The rest of the `tabs` API can be used without requesting any permission.
  - As of Firefox 86 and Chrome 50, matching [host permissions](#host_permissions) can also be used instead of the "tabs" permission.

- `webRequestBlocking` enables you to use the `"blocking"` argument, so you can [modify and cancel requests](/en-US/docs/Mozilla/Add-ons/WebExtensions/API/webRequest).
- `downloads.open` lets you use the {{WebExtAPIRef("downloads.open()")}} API.
- `tabHide` lets you use the {{WebExtAPIRef("tabs.hide()")}} API.

## activeTab permission

This permission is specified as `"activeTab"`. If an extension has the `activeTab` permission, then when the user interacts with the extension, the extension is granted extra privileges for the active tab only.

"User interaction" includes:

- the user clicks the extension's {{webextAPIref("browserAction", "browser action", "", 1)}} or [page action](/en-US/docs/Mozilla/Add-ons/WebExtensions/user_interface/Page_actions)
- the user selects its context menu item
- the user activates a keyboard shortcut defined by the extension

The extra privileges are:

- The ability to inject JavaScript or CSS into the tab programmatically (see [Loading content scripts](/en-US/docs/Mozilla/Add-ons/WebExtensions/Content_scripts#loading_content_scripts)).
- Access to the privileged parts of the tabs API for the current tab: `Tab.url`, `Tab.title`, and `Tab.faviconUrl`.

The intention of this permission is to enable extensions to fulfill a common use case, without having to give them very powerful permissions. Many extensions want to "do something to the current page when the user asks".

For example, consider an extension that wants to run a script in the current page when the user clicks a browser action. If the `activeTab` permission did not exist, the extension would need to ask for the host permission `<all_urls>`. But this gives the extension more power than it needs: it could now execute scripts in _any tab_, _any time_ it likes, instead of just the active tab and only in response to a user action.

> [!NOTE]
> You can only get access to the tab/data that was there, when the user interaction occurred (e.g., the click). When the active tab navigates away (e.g., due to finishing loading or some other event), the permission does not grant you access to the tab anymore.

The `activeTab` permission enables scripting access to the top level tab's page and same origin frames. Running scripts or modifying styles inside [cross-origin](/en-US/docs/Web/Security/Same-origin_policy#cross-origin_network_access) frames may require additional [host permissions](#host_permissions). Of course, [restrictions and limitations](/en-US/docs/Mozilla/Add-ons/WebExtensions/Content_scripts#permissions_restrictions_and_limitations) related to particular sites and URI schemes are applied as well.

Usually the tab that's granted `activeTab` is just the currently active tab, except in one case. The {{webextAPIref("menus")}} API enables an extension to create a menu item which is shown if the user context-clicks on a tab (that is, on the element in the tabstrip that enables the user to switch from one tab to another).

If the user clicks such an item, then the `activeTab` permission is granted for the tab the user clicked, even if it's not the currently active tab (as of Firefox 63, [Firefox bug 1446956](https://bugzil.la/1446956)).

## Clipboard access

There are two permissions which enables the extension to interact with the clipboard:

- `clipboardWrite`
  - : Write to the clipboard using {{DOMxRef("Clipboard.write()")}}, {{DOMxRef("Clipboard.writeText()")}}, `document.execCommand("copy")` or `document.execCommand("cut")`
- `clipboardRead`
  - : Read from the clipboard using {{DOMxRef("Clipboard.read()")}}, {{DOMxRef("Clipboard.readText()")}} or `document.execCommand("paste")`

See [Interact with the clipboard](/en-US/docs/Mozilla/Add-ons/WebExtensions/Interact_with_the_clipboard) for more details.

## Unlimited storage

The `unlimitedStorage` permission:

- Enables extensions to exceed any quota imposed by the {{WebExtAPIRef("storage/local", "storage.local")}} API
- In Firefox, enables extensions to create a ["persistent" IndexedDB database](/en-US/docs/Web/API/IndexedDB_API) without the browser prompting the user for permission at the time the database is created.

## Examples

```json
 "permissions": ["*://developer.mozilla.org/*"]
```

In Manifest V2 only, request privileged access to pages under `developer.mozilla.org`.

```json
  "permissions": ["tabs"]
```

Request access to the privileged pieces of the `tabs` API.

```json
  "permissions": ["*://developer.mozilla.org/*", "tabs"]
```

In Manifest V2 only, request both of the above permissions.

## Browser compatibility

{{Compat}}
