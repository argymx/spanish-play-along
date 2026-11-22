# Browser and device support

What works where, and why. Checked November 2026.

The site needs three things from a browser: a Spanish text to speech voice, microphone capture, and audio recording. Where a platform fails, it almost always fails on one of those rather than on the page itself.

## Summary

| Device | Browser | Listen, gaps, drills, advice | Record and compare |
|---|---|---|---|
| Windows | Edge | Yes | Yes |
| Windows | Chrome | Yes | Yes |
| Windows | Firefox | Yes | Yes |
| Mac | Chrome, Edge, Firefox | Yes | Yes |
| Mac | Safari | Yes | Yes |
| Android phone or tablet | Chrome | Yes, after voice setup | Yes |
| Android | Samsung Internet | Yes, after voice setup | Yes |
| Android | Firefox | Yes | Yes |
| Android | Opera Mobile | **No voice** | Yes |
| iPhone or iPad | Safari, Chrome, Firefox, Edge | Yes, with a poor voice | **No** |

**Best for pupils: a Windows laptop with Edge or Chrome.** Everything works, the Spanish voices are good, and no setup is required.

## Windows

Nothing to report, which is the point. Chrome, Edge and Firefox all support speech synthesis and recording, and Windows ships good Spanish voices. Edge adds its own online neural voices, which are the most natural of the lot. This is the recommended platform.

## macOS

All four major browsers work. Choose **Mónica** under More options: it is Apple's proper Spanish voice. The page now prefers it automatically, which matters because macOS also ships a set of novelty voices (Eddy, Flo, Grandma, Grandpa, Rocko and others) in every language, and they sort to the top alphabetically.

Note that a desktop Mac has no built in microphone, so recording needs headphones with a mic, a USB microphone or a webcam.

## Android

Recording works. The voice needs attention.

Chrome on Android lists voices for languages whose voice pack is not actually installed, so a Spanish voice can appear in the list and then produce nothing. If the model is silent, install the Spanish data: Settings, then Accessibility or Language, then Text to speech output, then the Google speech services voice data.

The first utterance after a page loads can also be slow on Android, occasionally by a long way, so give it a moment before concluding it is broken.

Firefox on Android supports speech synthesis and records normally. Opera Mobile does not expose speech synthesis at all, so the model voice will not work there.

## iPhone and iPad

**Record and compare does not work, and cannot be made to work from the page.**

There is a fault in WebKit, reported in 2020 and still open, where calling `speechSynthesis.speak` mutes an active `getUserMedia` audio track. The track is never unmuted and there is no way for page code to unmute it. Since this site speaks and then records, the recording comes back silent. A WebKit fix was opened in November 2026, so this should eventually resolve, but it is not in shipping Safari yet.

Switching browser does not help. Every browser on iOS is required to use Safari's engine, so Chrome, Firefox and Edge on an iPhone behave identically to Safari.

The voice is also weak on iOS. The browser is only shown Apple's Eloquence voice set, which is the novelty voices, rather than the proper system voices, so the Spanish model sounds like a cartoon.

**What still works on an iPad, and it is most of the value:** listening, the adjustable speed, the gaps to speak into, looping, all the drills, uploading your own material, and all the sound advice. Pupils simply speak into the gaps out loud rather than recording themselves. Attaching a clip recorded in Voice Memos from a phrase's `⋯` menu also works, so compare is available by that route.

The page detects iOS and says all of this on arrival rather than failing silently.

## Things that break on any platform

**A `file://` address.** Opening the HTML straight from disk means Chrome and Safari refuse the microphone by design, without prompting. Use the hosted address, or serve the folder with `python3 -m http.server`.

**An embedded frame.** A page inside an iframe is refused microphone permission. Safari refuses `getUserMedia` from a frame outright.

**A permission already set to denied.** Once a browser records a denial for a site it never prompts again, so the button appears to do nothing. Clear it from the icon at the left of the address bar, and check the operating system's own microphone privacy settings, which block silently too.

The **Check microphone** button on the page reports all of these by name.
