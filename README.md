# Chrome extension API for Safari and Firefox

With these two API's you can make Chrome extensions and use the same code and manifest in Safari and Firefox.
If you have more than one '*' in your urls in the manifest Firefox or Safari (I don't remember) fails.

The manifest parser for Firefox is the same as main.js.

Safari:

- Build an extension with the extension builder and set the web_accessible_resources the same as in your manifest.json.
  Maybe the permissions can be parsed from manifest.json, but for now you have to do it manually. You can also edit the           info.plist:
```
<key>Permissions</key>
	<dict>
		<key>Website Access</key>
		<dict>
			<key>Include Secure Pages</key>
			<true/>
			<key>Level</key>
			<string>All</string>
		</dict>
	</dict>
```
	
- Copy the chromeAPISafari directory, your js directory and the manifest.json to your Safari extension.

- Add the chromeAPISafari to extensionName.html, it should look like this:

```
<!DOCTYPE html>
<html>
<head>
    <title>Hello World</title>
    <script type="text/javascript" src="chromeAPISafari/chromeManifestSimulatorSafari.js"></script>
    <script type="text/javascript" src="chromeAPISafari/chromeAPIForSafari.js"></script>
    <script type="text/javascript" src="js/background.js"></script>
</head>
<body>Hello World!</body>
</html>
```

If you inject css with fonts you need to use .ttf instead of .wof
If you have only used Chrome Api's defined in the ChromeAPIForSafari.js, it should work.

Firefox:

ChromeApiForFirefox have a hack to follow a tab which is moved between windows. I found no better solution, and the solution does not work in FirefoxDeveloperEdition where you eventually lose the tab reference. For some strange reason, tab id change when moving tab to another window.

I used the cfx init, but I see that tool is deprecated. But I think you can do jpm init,
choose the chromeApiForSafari/chromeManifestSimulatorFirefox.js as your entry point.
Make a data directory, then copy all your files (js directory, html, img..) into the data directory.

If you inject css with fonts you need to use dataURL instead.
If you have only used Chrome Api's defined in the ChromeAPIForFirefox.js, it should work.

Things I want to add:

- chrome.browserAction    It should be possible to parse popup information from manifest.json.
  https://developer.mozilla.org/en-US/Add-ons/SDK/High-Level_APIs/panel#Attaching_panels_to_buttons
 https://developer.apple.com/library/safari/documentation/Tools/Conceptual/SafariExtensionGuide/AddingPopovers/AddingPopovers.html

- Grunt/Gulp task for building Safari And Firefox extension and a Yeoman generator :)

I will include a sample later.
