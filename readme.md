# [fullscreen web app wrong height](https://bugs.chromium.org/p/chromium/issues/detail?id=1013888)

Elements in fullscreen web apps on Android Chrome v77.0.3865.116 cannot always be sized to fullscreen.

## Reproduction Steps

1. Serve the web app and visit on Android Chrome. E.g., `live-server --host=192.168.1.42`.

   <a href=screenshot-2019-10-12-12-18-59-698479169.png><img src=screenshot-2019-10-12-12-18-59-698479169.png width=256></a>

1. Install the web app on your home screen.

   <a href=screenshot-2019-10-12-12-19-28-962797859.png><img src=screenshot-2019-10-12-12-19-28-962797859.png width=256></a> <a href=screenshot-2019-10-12-12-20-02-719674082.png><img src=screenshot-2019-10-12-12-20-02-719674082.png width=256></a>

1. Launch the web app and rotate to landscape.
1. Press the home virtual button and note the orientation reverts to portrait.

   <a href=screenshot-2019-10-12-12-23-52-152356504.png><img src=screenshot-2019-10-12-12-23-52-152356504.png width=256></a>

1. Swipe the home screen right to open the Google feed (or visit another app but this may reproduce less reliably).

   <a href=screenshot-2019-10-12-12-24-27-142614700.png><img src=screenshot-2019-10-12-12-24-27-142614700.png width=256></a>

1. Swipe back.

   <a href=screenshot-2019-10-12-12-24-36-668093605.png><img src=screenshot-2019-10-12-12-24-36-668093605.png width=256></a>

1. Launch the web app without changing the orientation. The blue canvas should completely cover the red body but doesn't.

   <a href=screenshot-2019-10-12-12-24-45-685968170.png><img src=screenshot-2019-10-12-12-24-45-685968170.png width=256></a>

## Notes
- In this scenario, `screen.height` is correct but all other height measurements including `document.documentElement.clientHeight` are incorrect.
- The body is visible and correctly fullscreen but the canvas element cannot be resized to match.
- The issue does not seem to occur when using `"display": "standalone"` instead of `"fullscreen"`. I was unable to discover a workaround.
- The issue resolves on orientation change but this is not possible for a fullscreen game app specifying a fixed orientation.
