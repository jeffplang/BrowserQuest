Bootstrap process
=================
* Upon load of index.html, the app is kicked off by the load of `require-jquery.js` at the bottom of the document.  This script reads the data-main attribute of its `<script>` tag and loads `home.js`.
* `home.js` loads `Class`, `Underscore`, `Stacktrace`, and `Util` modules.  It then requires `main.js`.
* `main.js` loads `JQuery`, and `App`.  It defines the `initApp()` function and runs it.

initApp() -- main.js
====================
* Creates a global App object

* Does browser detection, adds identifier classes to <body>

* Sets up event handlers on HTML/non-canvas elements (all are click handlers unless otherwise noted).  Most of these are related to the Parchments and various screens contained within:
|
|  * $('body') -- If Credits or About screens are present, this is the handler for "click anywhere to close"
|
|  * $('.barbutton') -- Refers to buttons along the bottom of the in-game HUD, toggles an "active" class on them
|
|  * $('#chatbutton') -- TODO: figure out what it does.  Show/hide chat input?
|
|  * $('#helpbutton') -- Toggles About screen
|
|  * $('#achievementsbutton') -- Toggles Achievements screen.  This button blinks when you get your first achievement.  If it's blinking, this handler will also disable that
|
|  * $('#instructions') -- hides all windows
|
|  * $('#playercount') -- Toggles Population Info screen
|
|  * $('#population') -- Toggles Population Info screen
|
|  * $('.clickable') -- Stops event propagation on anything with this class, so all clicks are handled within application js.  Smart.
|
|  * $('#toggle-credits') -- Toggle Credits screen
|
|  * $('#create-new span') -- If you have an existing character, clicking this brings up a new screen or something
|
|  * $('.delete') -- Deletes anything in the Storage module (which uses localStorage or cookies to store your character info) and takes you to the character creation screen
|
|  * $('#cancel span') -- Goes back to Select Character screen if user clicks "Cancel" on Delete Character screen
|
|  * $('.ribbon') -- Toggles About screen
|
|  * $('#nameInput') -- Keyup event on an <input>, checks if <input> has a value.  If so, enable the Play button.  If not, disable/keep disabled.
|
|  * $('#prev') and $('#next') -- Used for scrolling through achievements list
|
|  * $('#notifications div') -- Deals with notifications bar on the bottom (e.g. "You have killed a rat.")  
|      TODO: Add this description to the showMessage() documentation
|      Wrapper contains 2 vertically-aligned spans, #message1 and #message2.  When app.showMessage(msg) is called, it sets the text of #message2 to msg,
|      adds the class "top" to the wrapper, which triggers a CSS3 transition to slide it up a few pixels.  This provides the effect of the message
|      "sliding up" into the notification bar window.  When the transition is complete, this documented binding removes the class "top" (no transition occurs here?),
|      and sets the text of #message2 to #message1.  showMessage() also sets a timeout of 5secs to add the "top" class to the wrapper again, which triggers
|      the message copying (#message2 will now be blank in most cases, so it will make #message1 also blank) and eventually the removal of the "top" class.
|      Very clever way of showing a seemingly endless stream of messages scrolling up from the bottom.
|
|  * $('.close') -- Closes all open screens
|
|  * $('.twitter') and $('.facebook') -- Opens a new browser window for sharing the game on these social networks
|

* Checks Storage to see if user has already played.  If so, it shows the player name and picture instead of an input.

* Sets up the Play button click handler.  Runs app.tryStartingGame when you click it!

* Adds an event listener to "touchstarted" event.  Not sure what the default behavior is, but this kills it.  Maybe to prevent scrolling 
  or something?  TODO: Disable this and see what breaks.

* Sets up resize detection.  When the browser viewport gets resized, #resize-check's height will change based on its definitions in the various 
  screen size media queries.  A near-instantaneous CSS3 transition is defined #resize-check, so these bindings occur when that finishes.  It 
  resizes the in-game UI through Javascript (must not be able to do it with media queries for some reason?)

* Logs a message and kicks off initGame()!