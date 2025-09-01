# Server `fetch` API error handling repro

The server `fetch` API throws an error instead of returning a response for
non-successful HTTP status codes (e.g., 404).

The endpoint added in [this commit](https://github.com/blaugold/fetch-repro/commit/8d8559a5736dbe218368f1a5002373daa4a71079)
should show a toast with the status code of the response, but instead it encounters an error:

```
[DEVVIT] Error fetching from random.org Error: 2 UNKNOWN: Get "https://www.random.org/foobar": httpbp.ClientError: http status 404 Not Found: <!DOCTYPE html>
[DEVVIT] <html lang="en-US">
[DEVVIT]   <head>
[DEVVIT]
[DEVVIT]     <meta charset="utf-8" />
[DEVVIT]     <meta name="referrer" content="strict-origin-when-cross-origin" />
[DEVVIT]     <meta name="viewport" content="width=device-width, initial-scale=1" />
[DEVVIT]     <meta id="request-method" name="request-method" content="GET" />
[DEVVIT]     <meta http-equiv="X-UA-Compatible" content="IE=edge">
[DEVVIT]     <meta name="description" content="The page you requested was not found.">
[DEVVIT]     <meta name="twitter:card" content="summary" />
[DEVVIT]     <meta name="twitter:site" content="@RandomOrg" />
[DEVVIT]     <meta name="twitter:title" content="404 - Page Not Found" />
[DEVVIT]     <meta name="twitter:description" content="The page you requested was not found." />
[DEVVIT]     <meta name="twitter:image" content="https://www.random.org/graphics/rdo-icon-white.png" />
[DEVVIT]     <meta property="og:site_name" content="RANDOM.ORG" />
[DEVVIT]     <meta property="og:title" content="404 - Page Not Found">
[DEVVIT]     <meta property="og:type" content="article">
[DEVVIT]     <meta property="og:image" content="https://www.random.org/graphics/rd
[DEVVIT]     at callErrorFromStatus (/srv/index.cjs:5299:21)
[DEVVIT]     at Object.onReceiveStatus (/srv/index.cjs:5980:70)
[DEVVIT]     at Object.onReceiveStatus (/srv/index.cjs:5782:140)
[DEVVIT]     at Object.onReceiveStatus (/srv/index.cjs:5748:175)
[DEVVIT]     at /srv/index.cjs:15425:74
[DEVVIT]     at process.processTicksAndRejections (node:internal/process/task_queues:85:11)
[DEVVIT] for call at
[DEVVIT]     at Client3.makeUnaryRequest (/srv/index.cjs:5950:32)
[DEVVIT]     at /srv/index.cjs:127518:61
[DEVVIT]     at /srv/index.cjs:127578:5
[DEVVIT]     at new Promise (<anonymous>)
[DEVVIT]     at GrpcWrapper._GrpcWrapper_promiseWithGrpcCallback2 (/srv/index.cjs:127576:10)
[DEVVIT]     at GrpcWrapper.request (/srv/index.cjs:127517:109)
[DEVVIT]     at GenericPluginClient.Fetch (/srv/index.cjs:127871:93)
[DEVVIT]     at fetch2 (/srv/index.cjs:125483:44)
[DEVVIT]     at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
[DEVVIT]     at async main.js:128598:23 {
[DEVVIT]   code: 2,
[DEVVIT]   details: 'Get "https://www.random.org/foobar": httpbp.ClientError: http status 404 Not Found: <!DOCTYPE html>\n' +
[DEVVIT]     '<html lang="en-US">\n' +
[DEVVIT]     '  <head>\n' +
[DEVVIT]     '    \n' +
[DEVVIT]     '    <meta charset="utf-8" />\n' +
[DEVVIT]     '    <meta name="referrer" content="strict-origin-when-cross-origin" />\n' +
[DEVVIT]     '    <meta name="viewport" content="width=device-width, initial-scale=1" />\n' +
[DEVVIT]     '    <meta id="request-method" name="request-method" content="GET" />\n' +
[DEVVIT]     '    <meta http-equiv="X-UA-Compatible" content="IE=edge">\n' +
[DEVVIT]     '    <meta name="description" content="The page you requested was not found.">\n' +
[DEVVIT]     '    <meta name="twitter:card" content="summary" />\n' +
[DEVVIT]     '    <meta name="twitter:site" content="@RandomOrg" />\n' +
[DEVVIT]     '    <meta name="twitter:title" content="404 - Page Not Found" />\n' +
[DEVVIT]     '    <meta name="twitter:description" content="The page you requested was not found." />\n' +
[DEVVIT]     '    <meta name="twitter:image" content="https://www.random.org/graphics/rdo-icon-white.png" />\n' +
[DEVVIT]     '    <meta property="og:site_name" content="RANDOM.ORG" />\n' +
[DEVVIT]     '    <meta property="og:title" content="404 - Page Not Found">\n' +
[DEVVIT]     '    <meta property="og:type" content="article">\n' +
[DEVVIT]     '    <meta property="og:image" content="https://www.random.org/graphics/rd',
[DEVVIT]   metadata: _Metadata { internalRepr: Map(0) {}, options: {} }
[DEVVIT] }
```
