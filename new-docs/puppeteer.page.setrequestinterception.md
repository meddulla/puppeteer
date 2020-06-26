<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [puppeteer](./puppeteer.md) &gt; [Page](./puppeteer.page.md) &gt; [setRequestInterception](./puppeteer.page.setrequestinterception.md)

## Page.setRequestInterception() method

<b>Signature:</b>

```typescript
setRequestInterception(value: boolean): Promise<void>;
```

## Parameters

|  Parameter | Type | Description |
|  --- | --- | --- |
|  value | boolean | Whether to enable request interception. |

<b>Returns:</b>

Promise&lt;void&gt;

## Remarks

Activating request interception enables [HTTPRequest.abort()](./puppeteer.httprequest.abort.md)<!-- -->, [HTTPRequest.continue()](./puppeteer.httprequest.continue.md) and [HTTPRequest.respond()](./puppeteer.httprequest.respond.md) methods. This provides the capability to modify network requests that are made by a page.

Once request interception is enabled, every request will stall unless it's continued, responded or aborted.

\*\*NOTE\*\* Enabling request interception disables page caching.

## Example

An example of a naïve request interceptor that aborts all image requests:

```js
const puppeteer = require('puppeteer');
(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.setRequestInterception(true);
  page.on('request', interceptedRequest => {
    if (interceptedRequest.url().endsWith('.png') ||
        interceptedRequest.url().endsWith('.jpg'))
      interceptedRequest.abort();
    else
      interceptedRequest.continue();
    });
  await page.goto('https://example.com');
  await browser.close();
})();

```
