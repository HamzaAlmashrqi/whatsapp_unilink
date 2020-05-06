# `whatsapp_unilink`

> Dart package helping your app interact with WhatsApp via HTTP links (universal links). Works with Flutter.

The `whatsapp_unilink` package helps you build HTTP links and provides you with an idiomatic Dart interface that:

* converts your phone number into something that WhatsApp expects ✅
* hides the encoding and link building details from you so that you can focus on your app 🚀
* is blazingly fast ⚡️

## Important links

* [Read the source code and **star the repo!** on GitHub](https://github.com/dartsidedev/whatsapp_unilink)
* [Open an issue on GitHub](https://github.com/dartsidedev/whatsapp_unilink/issues)
* [See package on `pub.dev`](https://pub.dev/packages/whatsapp_unilink)
* [Read the docs on `pub.dev`](https://pub.dev/documentation/whatsapp_unilink/latest/)

#### About WhatsApp links

* [WhatsApp FAQ > Android > How to use click to chat](https://faq.whatsapp.com/en/android/26000030/)
* [WhatsApp FAQ > iPhone > How to link to WhatsApp from a different app](https://faq.whatsapp.com/en/iphone/23559013)

## Usage

With `WhatsAppUnilink`, you can create a link that will allow your users to start a chat with someone (identified with `phoneNumber`).
By clicking the link, a chat with the person automatically opens.
WhatsApp will include your message in `text` and it will automatically appear in the text field of a chat.

Both the `phoneNumber` and `text` arguments are optional.
The `phoneNumber` string will be internally converted to a format that the WhatsApp API expect: any brackets, dashes, plus signs, and leading zeros or any other non-digit characters will be removed.
The `text` is encoded using percent-encoding to make it safe for literal use as a URI component.
The `WhatsAppUnilink` instance, whenever converted to a string, will create a WhatsApp link for you.

### Flutter

You may want to launch the WhatsApp app on your user's phone and make life easier for your users by pre-filling the mobile number and text. Use the [`url_launcher`](https://pub.dev/packages/url_launcher) for launching the links you create with the `whatsapp_unilink` package.

```dart
import 'package:whatsapp_unilink/whatsapp_unilink.dart';
// For Flutter applications, you'll most likely want to use
// the url_launcher package.
import 'package:url_launcher/url_launcher.dart';

// ...somewhere in your Flutter app...
launchWhatsApp() async {
  final link = WhatsAppUnilink(
    phoneNumber: '+001-(555)1234567',
    text: "Hey! I'm inquiring about the apartment listing",
  );
  // Convert the WhatsAppUnilink instance to a string.
  // Use either Dart's string interpolation or the toString() method.
  // The "launch" method is part of "url_launcher".
  await launch('$link');
}
```

### Dart

This package works everywhere and doesn't have any Flutter-specific dependency.
It works on the frontend with AngularDart, or rendered to an `a` tag from your HTTP server.