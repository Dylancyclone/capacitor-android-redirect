(This is a reproduction repo for this issue: https://github.com/ionic-team/capacitor/issues/7454)

Capacitor on Android detected as web platform after redirecting with `allowNavigation`

After redirecting to an external URL that is allowed in the `server.allowNavigation` config setting, ([`./capacitor.config.json` line 7](https://github.com/Dylancyclone/capacitor-android-redirect/blob/main/capacitor.config.json#L7)) an android app reports being on a web platform instead of android.
This can be seen by calling `Capacitor.getPlatform()` ([`src/js/capacitor-welcome.js` line 67](https://github.com/Dylancyclone/capacitor-android-redirect/blob/main/src/js/capacitor-welcome.js#L67)) (which returns `android` before redirecting and `web` after redirecting) or by trying to use a native API, which will either fallback to the web version of the API, or fail to run at all ([`src/js/capacitor-welcome.js` line 91 and 106](https://github.com/Dylancyclone/capacitor-android-redirect/blob/main/src/js/capacitor-welcome.js#L106))

The redirection happens in [`src/js/capacitor-welcome.js` on line 70](https://github.com/Dylancyclone/capacitor-android-redirect/blob/main/src/js/capacitor-welcome.js#L70)

All this works on iOS, where after redirecting, the app can still use native iOS APIs

## To run the reproduction yourself

1. Clone this repository
2. Edit [`./capacitor.config.json` line 7](https://github.com/Dylancyclone/capacitor-android-redirect/blob/main/capacitor.config.json#L7) and [`./src/js/capacitor-welcome.js` line 70](https://github.com/Dylancyclone/capacitor-android-redirect/blob/main/src/js/capacitor-welcome.js#L70) to your computer's local IP address. (keep port 3000)
3. Run `yarn install` or `npm install`
4. Run `yarn build` or `npm build`
5. `cd dist` and `npx serve .` to start "production"/remote server
6. Install onto device or simulator of choice
7. Notice on android the platform is `android` and on iOS the platform is `ios` (you can also click on the "Take Photo" button to see the native API working)
8. Click the redirect button and notice on android the platform changes to `web` while on iOS it stays `ios` (you can also click on the "Take Photo" button to see the native API not working on Android, while still working on iOS)

---
*Original, Capacitor-generated README*

## Created with Capacitor Create App

This app was created using [`@capacitor/create-app`](https://github.com/ionic-team/create-capacitor-app),
and comes with a very minimal shell for building an app.

### Running this example

To run the provided example, you can use `npm start` command.

```bash
npm start
```
