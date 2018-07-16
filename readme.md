# getsmscode

> API client for [getsmscode.com](http://www.getsmscode.com/).

[![NPM](https://img.shields.io/npm/v/getsmscode.svg)](https://www.npmjs.com/package/getsmscode) [![Build Status](https://travis-ci.com/transitive-bullshit/getsmscode.svg?branch=master)](https://travis-ci.com/transitive-bullshit/getsmscode) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

-   provides temporary, physical mobile numbers (not virtual VOIP numbers!)
-   meant for automated systems that need to bypass SMS number verification
-   handles hundreds of known services (wechat, google, facebook, whatsapp, uber, twitter, etc...)

## Install

This module requires `node >= 8`.

```bash
npm install --save getsmscode
```

You'll need to setup a [getsmscode.com](http://www.getsmscode.com/) account and add some money to your account before using this module.

## Usage

```js
const GetSMSCodeClient = require('getsmscode')

const client = new GetSMSCodeClient({
  username: '...',
  token: '...'
})

const number = await client.getNumber({
  service: 'google'
})

// give this number to third-party service such as google...
// third-party service sends SMS code to the given number...

const sms = await client.getSMS({
  service: 'google',
  number: number
})
```

**Note**: there may be variable amounts of latency between giving your number to the service and the SMS code being received. If no valid messages are returned, it is recommended that you retry `client.getSMS` with an exponential timeout. Be careful not to call the API too fast, however, as `getsmscode` imposes strict rate limits.

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### [GetSMSCodeClient](https://github.com/transitive-bullshit/getsmscode/blob/e3a59494c4d4699af1d77e1cea0424da1b6f0e82/index.js#L43-L214)

Type: `function (opts)`

-   `opts` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** Config options
    -   `opts.username` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Username for getsmscode auth (optional, default `process.env.GETSMSCODE_USERNAME`)
    -   `opts.token` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Token for getsmscode auth (optional, default `process.env.GETSMSCODE_TOKEN`)
    -   `opts.domain` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Domain for this client to use (china/usa/asia) (optional, default `'china'`)

* * *

#### [login](https://github.com/transitive-bullshit/getsmscode/blob/e3a59494c4d4699af1d77e1cea0424da1b6f0e82/index.js#L71-L80)

Logs in to test auth and fetches an account summary.

Type: `function (): Promise`

* * *

#### [getNumber](https://github.com/transitive-bullshit/getsmscode/blob/e3a59494c4d4699af1d77e1cea0424da1b6f0e82/index.js#L94-L114)

Acquires a temporary handle on a mobile number usable for the given service.

You must specify either `opts.service` or `opts.pid`.

Type: `function (opts): Promise`

-   `opts` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Config options
    -   `opts.service` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Name of service to blacklist number
    -   `opts.pid` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Project ID of service to blacklist number
    -   `opts.cocode` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Country code (required if using asian domain)

* * *

#### [getNumbers](https://github.com/transitive-bullshit/getsmscode/blob/e3a59494c4d4699af1d77e1cea0424da1b6f0e82/index.js#L121-L131)

Returns a list of `{ number, service }` objects currently in use by this account.

Type: `function (): Promise`

* * *

#### [getSMS](https://github.com/transitive-bullshit/getsmscode/blob/e3a59494c4d4699af1d77e1cea0424da1b6f0e82/index.js#L145-L166)

You must specify either `opts.service` or `opts.pid`.

Type: `function (opts): Promise`

-   `opts` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Config options
    -   `opts.number` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Mobile number to blacklist
    -   `opts.service` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Name of service to blacklist number
    -   `opts.pid` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Project ID of service to blacklist number
    -   `opts.cocode` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Country code (required if using asian domain)

* * *

#### [addNumberToBlacklist](https://github.com/transitive-bullshit/getsmscode/blob/e3a59494c4d4699af1d77e1cea0424da1b6f0e82/index.js#L181-L196)

Adds a number to this account's blacklist for the given service.

You must specify either `opts.service` or `opts.pid`.

Type: `function (opts): Promise`

-   `opts` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Config options
    -   `opts.number` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Mobile number to blacklist
    -   `opts.service` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Name of service to blacklist number
    -   `opts.pid` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Project ID of service to blacklist number
    -   `opts.cocode` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Country code (required if using asian domain)

## Related

-   [sms-number-verifier](https://github.com/transitive-bullshit/sms-number-verifier) - Allows you to spoof SMS number verification.
-   [parse-otp-message](https://github.com/transitive-bullshit/parse-otp-message) - Parses OTP messages for a verification code and service provider.

## Disclaimer

Using this software to violate the terms and conditions of any third-party service is strictly against the intent of this software. By using this software, you are acknowledging this fact and absolving the author or any potential liability or wrongdoing it may cause. This software is meant for testing and experimental purposes only, so please act responsibly.

## License

MIT © [Travis Fischer](https://github.com/transitive-bullshit)
