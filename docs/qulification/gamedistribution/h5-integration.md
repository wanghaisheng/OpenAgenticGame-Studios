CONNECT YOUR GAME WITH OUR SDKs

Note for legacy users
Is your game still loading this URL? html5.api.gamedistribution.com/libs/gd/api.js, then do be aware that this is a legacy integration. However; the new SDK is backwards compatible, so no development action is required. Nonetheless make sure your game is still working properly on the Gamedistribution.com platform or upgrade your implementation to the new spec.

Implementation
Implement the following snippet within your game or within the <head> section of your index.html. The GD_OPTIONS object is safe to obfuscate if needed.

Make sure that the SDK is loaded before your game starts or while your game is loaded for the best user experience. Not after, and especially not by clicking a button within the game, as then it will take too long for an advertisement to load; making the user wait. Only load the SDK once!

window["GD_OPTIONS"] = {
    "gameId": "[YOUR GD GAME ID HERE]",
    "onEvent": function(event) {
        switch (event.name) {
            case "SDK_GAME_START":
                // advertisement done, resume game logic and unmute audio
                break;
            case "SDK_GAME_PAUSE":
                // pause game logic / mute audio
                break;
            case "SDK_GDPR_TRACKING":
                // this event is triggered when your user doesn't want to be tracked
                break;
            case "SDK_GDPR_TARGETING":
                // this event is triggered when your user doesn't want personalised targeting of ads and such
                break;
            case "SDK_REWARDED_WATCH_COMPLETE":
                // this event is triggered when your user completely watched rewarded ad
                break;
        }
    },
};
(function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s);
    js.id = id;
    js.src = 'https://html5.api.gamedistribution.com/main.min.js';
    fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'gamedistribution-jssdk'));
Mandatory settings:
Make sure to add your game hash (gameId), which you can retrieve from your Gamedistribution.com control panel.
Invoke a method to pause AND mute your game within the SDK_GAME_PAUSE event. Will be called every time a video advertisement is ready to play. It is important that the game is muted, as background audio through video advertisements is forbidden.
Invoke a method to resume your game within the SDK_GAME_START event. Will be called every time a video advertisement is done playing.
Invoke an advertisement
Correct ad-placement is key for a higher revenue potential of your game. Before you submit, make sure that your game includes a pre-roll and mid-rolls:

Pre-roll: an ad shown before the user starts playing the game.
What you basically want to do is display the pre-roll as fast as possible to the user, so they don’t have the time to change their minds and close the game.
Best practice: placing the pre-roll on buttons in the loading/splash screen (Start, Play, Continue).

Mid-roll: an ad shown in between game sessions.
Ideally placed on all non-gameplay buttons, to spread the chance that users will see ads.
Best practice: placing the mid-rolls on each button in the Game Over/Win screen (Replay, Next, Menu).

To get the most out of your game revenue and to maintain a user friendly experience, we ask you to keep these requirements in mind when deciding on the placement of the ads:

Ads only display upon user input, e.g. when clicking a button
Ads display outside of the gameplay only, to not disrupt the game experience
Game audio is muted when the ad is displayed
The game pauses when the ad is displayed
Don’t worry about spamming users with ads by placing ad-calls on too many buttons: we regulate the ad-interval through the SDK, so users will only see an ad when the set time-frame has passed.

Now, everything should be set up for you. All you need to do now in order monetize your game is to call gdsdk.showAd() at the appropriate time in your game. This showAd() call should be behind a touchUp/mouseUp event in order to work correctly on mobile and adhere by the ad rules.

Note: Make sure to check if the gdsdk instance exists and the showAd method exists as well. In case the SDK script goes offline or when adblocker stops it for whatever reason. Its just good practice when it comes to using third-party solutions.

nextButton.addEventListener('mouseUp', function () {
    if (typeof gdsdk !== 'undefined' && gdsdk.showAd !== 'undefined') {
         gdsdk.showAd();
    }
});
A lot of developers miss out on a lot of revenue by not calling so-called mid-roll advertisements. Do know that you can call the gdsdk.showAd(); method as often as you want. We make sure its not possible to call too many ads after another in order to uphold a proper user experience and advertisement guidelines.

gdsdk.showBanner() is DEPRECATED. It is still usable though. But for more features we recommend you to use new gdsdk.showAd() method.

Rewarded Ads
Users can watch an in-game video and receive rewards (like in-game currency, premium content, extra lives and credits, etc) in return. For detailed explanations: Rewarded Ads are here!

For instructions how to use, have a look at the page.

Display Ads
A display(banner) ad is a particular kind of online advertising resource that often shows up at the top or side of a webpage. It is an HTML construct that displays a given advertisement and, when clicked, takes the user to the advertiser's site.

For instructions how to use, have a look at the page.

Activate the SDK
To activate your SDK integration you will need to upload your game first (https://developer.gamedistribution.com/) and make sure you have uploaded your game.
You'll find your uploaded game URL at the bottom of the upload view within this admin. Here you'll also find a button to open your game within an iframe. Click this button.
You must completely view your new in-game pre-roll advertisement once, from within this iframe. Doing this will activate and verify the integration.
Your game will be flagged to have a valid integration of the SDK and your game can be requested for publishing. Please contact support if you're having any trouble concerning this step.


Go to the upload view, and after uploading your game, open it in an iframe by clicking the indicated button.



Your game will open within an iframe and a debugging bar will be displayed on top of your game.

A demo VAST tag for calling a fake advertisement is already enabled, so you only have to click the "showBanner" button, in order to request an advertisement.

Make sure you disable your ad blocker.

This VAST tag has a 99% fill rate, so if you don't get an ad, check your console log and either resolve any reported issues within your games, or if you can't fix it, contact our support team.



Make sure you completely watch the fake advertisement. Once the CONTENT_RESUME_REQUESTED event is triggered - without cancelling the advertisement - your game its SDK implementation will be approved. This can currently take up to two weeks.

Debugging
Games, which include the SDK, can be easily debugged by calling the following from a browser developer console:

gdsdk.openConsole();
This will open a tiny toolbar, which allows you to call fake advertisements, making the implementation much easier and reliable. Clear your localStorage to disable debugging.

Options
The GD_OPTIONS object allows the following properties:

Property	Description
gameId	our gameId which is unique for each one of your games; can be found at your Gamedistribution.com account.
prefix	Set your own prefix in case you get id conflicts.
advertisementSettings	Accepts an object of ad specific options.
Example:

window["GD_OPTIONS"] = {
    "gameId": "49258a0e497c42b5b5d87887f24d27a6",
    "prefix": "awesome__", // Set your own prefix in case you get id conflicts.
    "advertisementSettings": {
        "debug": false, // Enable IMA SDK debugging.
        "autoplay": false, // Don't use this because of browser video autoplay restrictions.
        "locale": "en", // Locale used in IMA SDK, this will localize the "Skip ad after x seconds" phrases.
    },
};
Events
SDK EVENTS
The SDK events should be used by developers to start or pause their game or handling critical errors. Unless the errors are ad related, then they could hook into the AD_ERROR event, however; the SDK should gracefully fail, so this should not be needed.

Event	Description
SDK_READY	When the SDK is ready.
SDK_ERROR	When the SDK has hit a critical error.
SDK_GAME_START	When the game should start.
SDK_GAME_PAUSE	When the game should pause.
SDK_GDPR_TRACKING	When the publishers' client has requested to not track his/ her data. Hook into this event to find out if you can record client tracking data.
SDK_GDPR_TARGETING	When the publishers' client has requested to not get personalized advertisements. Hook into this event to find out if you can display personalized advertisements in case you use another ad solution.
SDK_GDPR_THIRD_PARTY	When the publishers' client has requested to not load third party services. Hook into this event to find out if you can third party services like Facebook, AddThis, and such alike.
IMA SDK EVENTS
The SDK events are custom ads for handling any thing related to the IMA SDK itself.

Event	Description
AD_SDK_MANAGER_READY	When the adsManager instance is ready with ads.
AD_SDK_CANCELED	When the ad is cancelled or stopped because it's done running an ad.
AD EVENTS
The Gamedistribution.com SDK uses the IMA SDK for loading ads. All events of this SDK are also available to the developer. https://developers.google.com/interactive-media-ads/docs/sdks/html5/

Event	Description
AD_ERROR	When the ad it self has an error.
AD_BREAK_READY	Fired when an ad rule or a VMAP ad break would have played if autoPlayAdBreaks is false.
AD_METADATA	Fired when an ads list is loaded.
ALL_ADS_COMPLETED	Fired when the ads manager is done playing all the ads.
CLICK	Fired when the ad is clicked.
COMPLETE	Fired when the ad completes playing.
CONTENT_PAUSE_REQUESTED	Fired when content should be paused. This usually happens right before an ad is about to cover the content.
CONTENT_RESUME_REQUESTED	Fired when content should be resumed. This usually happens when an ad finishes or collapses.
DURATION_CHANGE	Fired when the ad's duration changes.
FIRST_QUARTILE	Fired when the ad playhead crosses first quartile.
IMPRESSION	Fired when the impression URL has been pinged.
INTERACTION	Fired when an ad triggers the interaction callback. Ad interactions contain an interaction ID string in the ad data.
LINEAR_CHANGED	Fired when the displayed ad changes from linear to nonlinear, or vice versa.
LOADED	Fired when ad data is available.
LOG	Fired when a non-fatal error is encountered. The user need not take any action since the SDK will continue with the same or next ad playback depending on the error situation.
MIDPOINT	Fired when the ad playhead crosses midpoint.
PAUSED	Fired when the ad is paused.
RESUMED	Fired when the ad is resumed.
SKIPPABLE_STATE_CHANGED	Fired when the displayed ads skippable state is changed.
SKIPPED	Fired when the ad is skipped by the user.
STARTED	Fired when the ad starts playing.
THIRD_QUARTILE	Fired when the ad playhead crosses third quartile.
USER_CLOSE	Fired when the ad is closed by the user.
VOLUME_CHANGED	Fired when the ad volume has changed.
VOLUME_MUTED	Fired when the ad volume has been muted.
