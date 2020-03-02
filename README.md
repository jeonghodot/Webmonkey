Ubuntu

There are some problems.

(node:78367) UnhandledPromiseRejectionWarning: Error: ENOENT: no such file or directory, open '/usr/local/lib/node_modules/webmonkey/node_modules/figlet/fonts/univers.flf'
    at Object.openSync (fs.js:457:3)
    at Object.readFileSync (fs.js:359:35)
    at Function.figlet.loadFontSync (/usr/local/lib/node_modules/webmonkey/node_modules/figlet/lib/node-figlet.js:48:23)
    at Function.me.textSync (/usr/local/lib/node_modules/webmonkey/node_modules/figlet/lib/figlet.js:732:43)
    at main$1 (/usr/local/lib/node_modules/webmonkey/bin/index.js:398:25)
    at Object.<anonymous> (/usr/local/lib/node_modules/webmonkey/bin/index.js:418:1)
    at Module._compile (internal/modules/cjs/loader.js:1158:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1178:10)
    at Module.load (internal/modules/cjs/loader.js:1002:32)
    at Function.Module._load (internal/modules/cjs/loader.js:901:14)
(node:78367) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). To terminate the node process on unhandled promise rejection, use the CLI flag `--unhandled-rejections=strict` (see https://nodejs.org/api/cli.html#cli_unhandled_rejections_mode). (rejection id: 1)
(node:78367) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.







<img src="media/logo.png" alt="Webmonkey" width="350">

> Robust and versatile headless monkey testing for the modern web with reproducible steps, error alerts, strategy sharing and many other good things.

![Travis](http://img.shields.io/travis/Wildhoney/Webmonkey.svg?style=for-the-badge)
&nbsp;
![npm](http://img.shields.io/npm/v/webmonkey.svg?style=for-the-badge)
&nbsp;
![License MIT](http://img.shields.io/badge/license-mit-lightgrey.svg?style=for-the-badge)
&nbsp;
![Coveralls](https://img.shields.io/coveralls/Wildhoney/Webmonkey.svg?style=for-the-badge)
&nbsp;
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=for-the-badge)](https://github.com/prettier/prettier)

It's important to remember that [monkey testing](https://en.wikipedia.org/wiki/Monkey_testing) should be used in conjunction with smarter tests such as [integration tests](https://en.wikipedia.org/wiki/Integration_testing).

![Screenshot](media/screenshot.png)

## Getting Started

Once `webmonkey` has been installed globally, you can begin testing by supplying the `--url` parameter you'd like to test. As that's the only required field, testing begins immediately and proceeds with 50 actions.

```console
foo@bar:~$ webmonkey --url https://news.bbc.co.uk/
```

For other parameters you can type `webmonkey --help` at any time.

### Authenticating

Oftentimes you'll want to authenticate before proceeding with the testing. In cases such as these `webmonkey` provides a hooks file where you export two optional functions &mdash; `create` and `destroy` &mdash; you can specify the location of the hooks file with the `--hooks` parameter.

The hooks file **must** be in the `*.mjs` format &ndash; for instance to authenticate on a fictitious website one might implement the following.

```javascript
export const create = async page => {
    await page.goto('https://www.example.com/');
    await page.focus('#username');
    await page.keyboard.type('webmonkey');
    await page.focus('#password');
    await page.keyboard.type('monkeynuts');
    await page.keyboard.press('Enter');
    await page.waitForNavigation({ waitUntil: 'networkidle0' });
};
```

## Meet the Team

Currently we have the following set of monkeys that perform various actions on your supplied domain:

* `clicker` performs clicks in random regions of the visible viewport.
* `networker` cycles through a list of preset network conditions.
* `scroller` scrolls the viewport to different areas of the page.
* `sizer` randomly selects a different height and width for the viewport.
* `toucher` similar to the `clicker` action but instead performs touches.
* `typer` focuses on random input fields and types random characters.
