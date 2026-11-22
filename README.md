# Spanish Play Along

Reading aloud and pronunciation practice for GCSE Spanish. A single HTML page, no build step, no accounts, no server.

A model voice reads a phrase, leaves a silence of the same length, and the pupil says it back. They then hear the model, themselves, and the model again, tick whatever did not match, and get a specific explanation and a drill for that sound.

The idea is borrowed from music teaching, where playing along with a model at a reduced tempo and looping the difficult bar is simply how practice works.

## What it does

- **Model voice** at 55 to 100 per cent speed, using whichever Spanish voice is installed on the device
- **Silences** matched to the length of the phrase just spoken, adjustable to a quarter or much longer
- **Repeats** of one phrase, up to six, for drilling a single sound
- **Record and compare**: model, you, model again, back to back
- **Timing feedback** only: whether you spoke, when you started, how long for. It never scores pronunciation
- **Sound advice**: thirteen features (rolled rr, tapped r, c and z as /θ/, j and g, ñ, ll and y, written accents, final syllable stress, b and v, pure vowels, linking, silent h, qu as k), each with the usual English speaker error, how to produce the sound, and a drill
- **Your own material**: drop in a Word file, a PDF or text, or paste it. Split into phrases automatically and tagged for sounds
- **Your own audio**: attach a native speaker recording as the model for any phrase, slowed without changing pitch
- **A link per set**, so one passage or drill can be set as homework

Six reading aloud passages across the usual GCSE themes, eight sound drills, and a set of fluency chunks. All the Spanish was written for this tool.

## Why no pronunciation score

Automated pronunciation scoring is least reliable on exactly the features that matter most here. Microsoft's own documentation for its Pronunciation Assessment notes that accents, learner speech and language specific phonetics such as nasal vowels and liaison are challenging, and that small changes in recording conditions shift the scores. A tool that marks a correctly pronounced sound wrong does more harm than no tool at all.

So the only measured feedback is timing, which cannot be wrong, and everything about the sounds themselves is a self check with concrete advice attached.

## Privacy

Nothing leaves the device. No audio, no text, no recordings, no accounts, no analytics, no cookies, no network requests except the optional libraries used to read Word and PDF files. Recordings exist in the browser tab's memory and are gone when the tab is closed.

The one piece of browser storage is a flag remembering that the three step introduction has been dismissed.

## Running it

Opening `index.html` straight from disk will not let you record: Chrome and Safari refuse the microphone to `file://` pages by design, without prompting. Either use the hosted address, or serve the folder locally:

```
cd path/to/this/folder
python3 -m http.server 8765
```

then visit `http://localhost:8765/`.

A page inside an embedded frame is refused the microphone too. Everything other than recording works in both cases, and a clip recorded in a voice recorder app can always be attached to a phrase from its `⋯` menu.

The page has a **Check microphone** button that reports the page address, whether it is framed, the permission state, every audio input it can see, the supported recording formats, and the result of a live test recording.

## Hosting

Any static host. For GitHub Pages, put `index.html` at the root of the repository and switch Pages on for the default branch. `.nojekyll` is there to stop Jekyll processing the folder.

## Adapting it

Everything is in one file. The two things worth editing:

- `SETS` holds the passages and drills. Each item is `{text, tags}`, where tags are keys from `SOUNDS`.
- `SOUNDS` holds the advice library. Each entry has the check question the pupil sees, what the sound is, how to produce it, and which drill to send them to.

Adding another language means a new `SOUNDS` library and a new `SETS` list. The engine itself is language agnostic.
