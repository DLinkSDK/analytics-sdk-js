## Analytics SDK

### Step 1: Get the Account ID and Dev Token

Register an account at https://console.dlink.cloud. After creating an app on the platform, Get the corresponding Account ID and Dev Token for App Setting.

### Step 2: Integrate the SDK and complete event reporting

JS-SDK: [https://jssdk.deeplink.dev/sdk/2.1.1/deeplink.min.js](https://jssdk.deeplink.dev/analytics/1.4.7-beta/analytics.min.js)

### Step 3: Initialize the SDK

```javascript

 (function (e, t, n) {
        if (e.analytics) return;
        var a = e.analytics = function () {
            a.handleRequest ? a.handleRequest.apply(a, arguments) : a.queue.push(arguments)
        };
        a.queue = [];
        var s = 'script';
        r = t.createElement(s);
        r.async = !0;
        r.src = n;
        var u = t.getElementsByTagName(s)[0];
        u.parentNode.insertBefore(r, u);
    })(window, document, 'https://jssdk.deeplink.dev/analytics/[your_version]/analytics.min.js');

    // * [require] setup config 
    analytics('setup', {
        accountId: "your_accountId",
        devToken: "your_devToken",
        cryptKey: "your_cryptKey",
        minReportInterval: 10, // unit: s
        maxReportNumEachTime: 50,
        enabledInterval: true,
        // debugMode: true
    })
```
### Step 4: Use the SDK

```javascript

    /// * [require] register custom sender
    analytics('register', {
        sender: function (pkg, finished) {
            try {
                console.log('report http client', {pkg});
                finished(true); // ack confirm
            } catch (e) {
                finished(false);
            }
        }
    })

    // report log
    analytics('log', "eventName", {"eventParams": "eventParams"}, 1)

    // flush
    analytics('flush');

```


### Quick Start

```html

<script type='text/javascript'>
    (function (e, t, n) {
        if (e.analytics) return;
        var a = e.analytics = function () {
            a.handleRequest ? a.handleRequest.apply(a, arguments) : a.queue.push(arguments)
        };
        a.queue = [];
        var s = 'script';
        r = t.createElement(s);
        r.async = !0;
        r.src = n;
        var u = t.getElementsByTagName(s)[0];
        u.parentNode.insertBefore(r, u);
    })(window, document, 'https://jssdk.deeplink.dev/analytics/[your_version]/analytics.min.js');

    // * [require] setup config 
    analytics('setup', {
        accountId: "your_accountId",
        devToken: "your_devToken",
        cryptKey: "your_cryptKey",
        minReportInterval: 10, // unit: s
        maxReportNumEachTime: 50,
        enabledInterval: true,
        // debugMode: true
    })


    /// * [require] register custom sender
    analytics('register', {
        sender: function (pkg, finished) {
            try {
                console.log('report http client', {pkg});
                finished(true); // ack confirm
            } catch (e) {
                finished(false);
            }
        }
    })

    // ======================================== other ==================================

    // add Custom Params
    analytics('addCustomParams', {});

    // report log
    analytics('log', "eventName", {"eventParams": "eventParams"}, 1)

    // flush
    analytics('flush');

</script>
```

