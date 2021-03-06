# jQuery.fbMessenger

*A jQuery plugin to easily visualize fake Facebook Messenger interactions, with an iPhone theme. Ideal for your bot landing page.*

[Click here to see it in action.](https://digitalbreed.github.io/jquery.fbmessenger/)

![Interaction produced by jQuery.fbMessenger](https://github.com/digitalbreed/jquery.fbmessenger/raw/develop/demo/jquery.fbmessenger.gif)

Please note that this plugin is meant for demonstration purposes only and was not built to reproduce a pixel-perfect Messenger experience.

## Usage Example

Simply include `jquery.fbmessenger.min.js` and `jquery.fbmessenger.css` in your project; then use `$.fn.fbMessenger` on the target element to initialize and schedule actions on it.

```html
<html>
<head>
  <script src="https://code.jquery.com/jquery-1.12.4.min.js"></script>
  <script src="jquery.fbmessenger.min.js"></script>
  <link rel="stylesheet" href="jquery.fbmessenger.css">
  <style>
    /**
      For the best possible result, the container should be sized similarly to an iPhone 6 (i.e. 750x1334 pixels or 1:1.79 aspect ratio).
    */
    .phone {
      width: 375px;
      height: 667px;
    }
</head>
<body>
  <div class="phone">
  </div>
  <script>
    $(function() {
      $('.phone')
        // Initialize the plugin
        .fbMessenger({
          // options go here
        })
        // Schedule some interaction:
        .fbMessenger('start', { delay: 1000 })
        .fbMessenger('message', 'user', 'Get Started', { delay: 250 })
        .fbMessenger('typingIndicator', { delay: 250 })
        .fbMessenger('message', 'bot', 'Hello my friend, I am a jQuery plugin to fake Messenger interactions! I hope you like it.', { delay: 1500 })
        .fbMessenger('typingIndicator', { delay: 0 })
        .fbMessenger('message', 'bot', 'If you find my services useful, please star me on GitHub!', { delay: 1500 })
        .fbMessenger('message', 'user', 'Hi, nice to meet you! I definitely will do!', { delay: 2000 })
        .fbMessenger('typingIndicator', { delay: 0 })
        .fbMessenger('message', 'bot', 'Really?', { delay: 1000 })
        .fbMessenger('showQuickReplies', [ 'Yes!', 'Maybe...', 'Nope, just wanted to be polite' ], { delay: 2000 })
        .fbMessenger('selectQuickReply', 0, { delay: 1000 })
        .fbMessenger('showButtonTemplate', 'Do you use button templates?', [ 'Yes', 'No' ], { delay: 1500 })
        .fbMessenger('selectButtonTemplate', 0, { delay: 2000 })
        .fbMessenger('showGenericTemplate', [
          {
            imageUrl: '/your-first-image.png',
            title: 'This is the first option.',
            subtitle: 'You can have a subtitle if you like.',
            buttons: [
              'Button 1',
              'Button 2'
            ]
          },
          {
            imageUrl: '/your-second-image.png',
            title: 'This is your second option. Subtitle is optional!',
            buttons: [
              'Button 3',
              'Button 4'
            ];
          }
        ], { delay: 2000 })
        .fbMessenger('scrollGenericTemplate', 1, { delay: 1000 })
        .fbMessenger('selectGenericTemplate', 0, { delay: 1000 })
        // And trigger the execution
        .fbMessenger('run');
      });
  </script>
</body>
</html>
```

## Methods

| Method | Description
| ------ | -----------
| `('start', options)` | Replaces the welcome screen with the actual chat in order to send messages, similarly as if the user touches the "Get Started" button.
| `('message', user, text, options)` | Creates a new message sent by user with symbolic name `user` with text `text` and (optional) timestamp `options.timestamp` (must be type `Date`).
| `('typingIndicator', options)` | Enables the typing indicator for the left user. It remains turned on until a new message is sent by the left user.
| `('showQuickReplies', quickReplies, options)` | Moves the quick reply options into view, where `quickReplies` is an array of strings.
| `('selectQuickReply', quickReplyIndex, options)` | Selects the quick reply with index `quickReplyIndex`.
| `('showButtonTemplate', text, buttons, options)` | Shows a button template with the given buttons, where `buttons` is an array of strings.
| `('selectButtonTemplate', buttonIndex, options)` | Selects the button with index `buttonIndex`.
| `('showGenericTemplate', templates, options)` | Shows a generic template with the given items, where `templates` is an array of objects `{ imageUrl: '...', title: '...', subtitle: '...', buttons: [ ... ] }` (see usage example).
| `('scrollGenericTemplate', templateIndex, options)` | Scrolls the generic template item with the given index into view.
| `('selectGenericTemplate', buttonIndex, options)` | Selects the button with the given `buttonIndex` on the generic template item which is currently in view.
| `('run')` | Executes the previously scheduled steps.

The `options` parameter is optional and may contain an attribute `delay`. If `delay` is provided, execution is halted until `run` is called and every step is delayed `delay` milliseconds to the previous step. If it's not provided, the corresponding action is executed immediately.

## Options

| Option | Description
| ------ | -----------
| `botLogoUrl` | URL of the image to display as the bot logo.
| `botName` | Name of the bot, appears in the navigation bar and in the bot information at the beginning of the chat.
| `botCategory` | Category of the bot, appears in the bot information below the bot name.
| `botWelcomeMessage` | A short welcome message displayed before the user initiates the conversation by clicking "Get Started".
| `leftUser` | Symbolic name of the left chat user (default `bot`). Used to identify the origin of a message.
| `rightUser` | Symbolic name of the right chat user (default `user`). Used to identify the origin of a  message.
| `displayedCarrier` | Carrier name displayed in the status bar.
| `displayedTime` | Time displayed in the status bar.
| `scrollTimeMs` | Time in milliseconds the left user's icon needs to move to the latest message in a series of subsequent messages (default `500`).
| `dateFormat` | `function` which takes the current date as a parameter and returns the formatted timestamp as a string.
| `loop` | Boolean indicating whether the run script should restart from the beginning once it is finished (default `true`).
| `script` | Array of steps to execute for scheduled execution.

## Roadmap

### Short term

I plan to work on these items very soon. If you need one of those to put jQuery.fbMessenger to good use, check back in a few days.

* Message sent/received/ last read indicator
* ~~Generic template support~~ (available since v0.0.4 2016-08-28)
* ~~Button template support~~ (available since v0.0.3 2016-08-23)
* ~~Quick replies~~ (available since v0.0.2 2016-08-22)
* Resize support
* Style updates
* Localization

### Long term

Better don't hold your breath for these ones. If you're in need of one of those, drop me a line or consider submitting these yourself in a PR.

* Fake keyboard input
* "Browser"
* Receipt template support
* Image/audio/file attachments
* Build an editor around it and allow exporting a HTML file, for people without any coding experience
* Airline templates (least priority, as they need lots of customization for very specific use cases)

## Legal

This project is a spare time project of Matthias Gall and in no way affiliated with Facebook.

"Facebook" is a registered trademark of Facebook, Inc., Menlo Park Calif., US. "iPhone" is a registered trademark of Apple Inc., Cupertino Calif., US. Other mentioned trademarks are trademarks of their respective owners.

Licensed under MIT license terms. See file LICENSE.
