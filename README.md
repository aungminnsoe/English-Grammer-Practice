# GrammarQuest 🚀

An unlimited English grammar trainer that runs in the browser and installs on your phone like a real app.
No accounts, no server, no internet needed after the first load. Everything is stored on your own device.

**76 grammar topics · A1 → C2 · questions generated fresh every time, so you never run out.**
**Plus a built-in dictionary: 613 words offline, any other word fetched once and kept for ever.**

---

## What's inside

| Area | What you get |
|---|---|
| 📖 **Learn** | Every topic has a short rule explanation, worked examples and two preview questions before you drill it. |
| 📕 **Words** | A dictionary you can search instantly, saved words, and flashcard review. See the section below. |
| ✍️ **Practice** | Adaptive sessions (10 / 25 / 50 questions). Topics you get wrong come back more often. Practise one level, one topic, or one exercise type. |
| 🎯 **Test** | Timed tests per level (15 Q / 8 min) plus a 30-question **Placement Test** that estimates your CEFR band. |
| 🎮 **Play** | Speed Round (60 s), Survival (3 lives, rising difficulty), Word Builder, Error Hunt and Level Ladder. |
| 🎁 **Daily Challenge** | 10 mixed questions, the same set all day, double XP, keeps your streak alive. |
| 📊 **Stats** | XP, levels and ranks, accuracy, mastery bars per level, a 14-day bar chart, a full **calendar heat map**, session history and 34 badges. |
| 👥 **Profiles** | Multiple learners on one device — each with their own XP, streak and history. Perfect for studying alongside someone else. |

### Five exercise formats, generated from every topic
- Multiple choice gap-fill
- Type the answer (no options shown)
- Word order — tap the words to rebuild the sentence
- Find the error — tap the wrong word
- Mixed, chosen automatically

## The dictionary 📕

Tap **WORDS** in the bottom bar, or the 🔍 button at the top of any screen, and start typing.

**613 words are built into the app** and need no internet at all:

- **105 irregular verbs** with all three forms (go · went · gone)
- **90 phrasal verbs** (put off, get by, look into…) with their formal one-word equivalents
- **41 easily confused pairs** — affect/effect, lend/borrow, lie/lay, fewer/less, its/it's
- **38 grammar terms** — gerund, participle, clause, subjunctive, inversion…
- **56 function words** — articles, prepositions, linkers, quantifiers
- **300+ everyday nouns, verbs, adjectives and adverbs**

Each entry gives the meaning, part of speech, forms, example sentences, similar words and a **"Watch out"** note for the mistake learners usually make. Many link straight to the matching grammar lesson.

**Smart search**

- Type an inflected form and it finds the base word: *went* → **go**, *children* → **child**, *bigger* → **big**
- Typos are forgiven: *recieve* → **receive**, *freind* → **friend**
- Search by meaning: type *postpone* and it finds **put off**

**Any word that isn't built in** is fetched once from a free online dictionary and then stored on your device permanently — so a word you look up on wifi still works on the bus.

**Saving and flashcards**

- Tap ⭐ on any word card to save it
- **Flashcard review** uses spaced repetition: words you know come back after 1, 2, 4, 8, 16 then 32 days; words you miss come back the same day
- Reviews earn XP and keep your daily streak alive, exactly like grammar questions
- Tap 🔊 on any word to hear it, using your phone's own voice (works offline)
- A **word of the day** waits for you on the Words tab

---

### Why it never runs out
Questions aren't stored in a list. Each topic is a small generator that recombines a bank of subjects, verbs (with all five forms), nouns, adjectives, time expressions and places. A single topic can produce thousands of different correct sentences, and the app picks the exercise format at random on top of that.

---

## Put it on GitHub Pages (5 minutes)

1. Create a new repository on GitHub — e.g. `grammarquest`. Make it **Public**.
2. Upload **all the files in this folder** to the root of the repo:
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
   - `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png`
   - `README.md`
3. Go to **Settings → Pages**.
4. Under *Build and deployment*, set **Source: Deploy from a branch**, **Branch: `main`**, folder **`/ (root)`**, then **Save**.
5. Wait about a minute. Your app is live at:
   `https://<your-username>.github.io/grammarquest/`

### Add it to your phone
- **Android / Chrome:** open the link → menu (⋮) → **Add to Home screen**.
- **iPhone / Safari:** open the link → Share button → **Add to Home Screen**.

It then opens full screen with no browser bars, and works with no signal.

### Sharing it with someone else
Just send them the same link. Their progress is saved separately in their own browser — nothing is shared between devices. If two people use the *same* phone, use **⚙️ Settings → Manage profiles** to give each person their own profile.

---

## Everyday use

- **Keep the streak.** One Daily Challenge a day is enough. The flame in the top bar shows your current streak; the calendar shows every day you studied.
- **Set a daily goal.** ⚙️ Settings → Daily goal. The ring on the home screen fills as you hit it.
- **Follow "Needs work".** The home screen lists your weakest topics; tapping one drills exactly that.
- **Take the Placement Test** now, and again in a month, to see your level move.

### Keyboard shortcuts (on a computer)
- `A` `B` `C` `D` or `1`–`4` — choose an answer
- `Enter` — continue to the next question

---

## Backups

Progress lives in your browser's local storage. Clearing site data or uninstalling the browser erases it.

- **⚙️ Settings → Export** downloads a `.json` backup.
- **⚙️ Settings → Import** restores it — also the way to move your progress to a new phone.

---

## Editing the app

Everything is in `index.html`: CSS at the top, then JavaScript in one `<script>` block, organised in numbered sections.

To add a grammar topic, copy an existing `topic({...})` block:

```js
topic({
  id: 'my-topic', lvl: 'B1', em: '🧠', name: 'My new topic',
  why: ['First rule line.', 'Second rule line.'],
  ex: ['An <em>example</em> sentence.'],
  gen() {
    const s = pick(SUBJ), v = pick(V);
    return mk(
      `${s.n} ___ ${v.c} every day.`,   // stem, with ___ for the gap
      s.sg ? v.s : v.b,                 // the correct answer
      [v.b, v.s, v.g, v.p],             // wrong options
      null,                             // full sentence (null = built automatically)
      `Explanation shown after answering.`
    );
  }
});
```

That's it — the new topic automatically appears in Learn, Practice, Tests and every game, in all five exercise formats.

To add dictionary words, find a block such as `DICT_CORE_A` and add a line. The fields are separated by `|`:

```
word | part of speech | definition | example ~ example | forms | synonyms | watch-out note | tags
```

```
mango|noun|a sweet tropical fruit with yellow flesh|I ate a mango.|plural: mangoes|||core,A1
```

Leave a field empty if you don't need it, but keep the `|` separators. Tags control which category the word appears under: `irr`, `phr`, `conf`, `gram`, `fn`, `core`, plus an optional level such as `B1`.

---

Built for daily study. Little and often beats one long session. 🔥
