# RingCentral Engage Voice JavaScript SDK

[![Build Status](https://travis-ci.com/ringcentral/engage-voice-js.svg?branch=release)](https://travis-ci.com/github/ringcentral/engage-voice-js)
[![Coverage Status](https://coveralls.io/repos/github/ringcentral/engage-voice-js/badge.svg?branch=release)](https://coveralls.io/github/ringcentral/engage-voice-js?branch=release)

RingCentral Engage Voice Client SDK for JavaScript.

## Features

- Auto refresh access token

## Use

```bash
npm i ringcentral-engage-voice-client
```

```js
const RingCentralEngageVoice = require('ringcentral-engage-voice-client').default
// or
// import RingCentralEngageVoice from 'ringcentral-engage-voice-client'

// create from ringcentral app client id /secret
// you can create app from https://developer.ringcentral.com
const ev = new RingCentralEngageVoice({
  clientId: process.env.RINGCENTRAL_CLIENTID,
  clientSecret: process.env.RINGCENTRAL_CLIENTSECRET
})

// auth with jwt
await ev.authorize({
  jwt: process.env.RINGCENTRAL_JWT
})

// get access token
const token = ev.token().accessToken

// can also auth with password flow
// await ev.authorize({
//   username: process.env.RINGCENTRAL_USERNAME,
//   extension: process.env.RINGCENTRAL_EXTENSION,
//   password: process.env.RINGCENTRAL_PASSWORD
// })

// can also auth with auth code flow
// check https://developers.ringcentral.com/guide/authentication for more detail
// await ev.authorize({
//   code: 'xxxx',
//   redirectUri: 'yyyyyy'
// })

// api request
// check all api doc from https://engage-voice-api-docs.readthedocs.io/en/latest/
let r = await ev.get('/api/v1/admin/accounts')
r = r.data
expect(r.length > 0).toBe(true)
```

For legacy server use:

```js
const RingCentralEngageVoice = require('ringcentral-engage-voice-client').default
// or
// import RingCentralEngageVoice from 'ringcentral-engage-voice-client'

// LEGACY_SERVER could be
// 'https://portal.vacd.biz',
// or  'https://portal.virtualacd.biz'
const ev = new RingCentralEngageVoice({
  server: process.env.LEGACY_SERVER
})

// only support username/password auth
await ev.authorize({
  username: process.env.LEGACY_USERNAME,
  password: process.env.LEGACY_PASSWORD
})

// api request
// check all api doc from https://engage-voice-api-docs.readthedocs.io/en/latest/
let r = await ev.get('/api/v1/admin/accounts')
r = r.data
expect(r.length > 0).toBe(true)

// revoke api token
ev.revokeLegacyToken()
```

## Instance methods

ev.request(config)

ev.get(url, config = {})

ev.post(url, data = undefined, config = {})

ev.put(url, data = undefined, config = {})

ev.delete (url, config = {})

ev.patch(url, data = undefined, config = {})

## Test

```bash
npm i
cp env-sample.env .env
# then edit .env fill all fields
npm run test
```

## Run demo code

```bash
cd demo
npm i
cp env-sample.env .env
# then edit .env fill all fields
npm start
# edit index.js to play
```

## Credits

Based on tyler's [ringcentral-js-concise](https://github.com/tylerlong/ringcentral-js-concise)

## License

MIT
