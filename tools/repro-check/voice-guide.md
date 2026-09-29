# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I am a student posting my own claim and my own reproduction on an issue in this repo. I am new to the codebase. A reader can expect the comment to name what I ran and what I saw, and to say so when I could not reproduce the issue.

## Rules I write by

### Rule: Name this issue's behavior

The claim names the failing behavior in this issue. A sentence that could be pasted onto a different issue does not go out.

- Wrong: "I'll take a look at this and try to reproduce it."
- Right: "I'll try to reproduce the 500 on POST /reviews when the rating field is omitted."

### Rule: Only claim what I ran

I say I reproduced something only after I have run it and the output shows it. If I have not run it, the comment says that.

- Wrong: "Confirmed, this still happens."
- Right: "I have not run this yet. I'll follow the steps on the issue and report what I see."

### Rule: My repro is my run

The repro comment carries my environment, my commands, and my output. I do not point at someone else's comment as my proof.

- Wrong: "Same as above, can confirm."
- Right: "On macOS 15.6 with Node 22.14.0 I ran `npm test` from a clean clone and got `TypeError: Cannot read properties of undefined (reading 'id')`."

### Rule: Separate what I saw from what I guess

The outcome sentence states only what the output shows. A cause is labeled as a guess.

- Wrong: "The bug is that the handler doesn't check for a missing rating."
- Right: "Observed: the response is 500 and the log says `rating is undefined`. Guess, not verified: the handler reads `rating` without a guard."

### Rule: No fix and no date

I do not promise a patch, a pull request, or a day. The comment stops at what I will observe.

- Wrong: "I'll have a fix up tonight."
- Right: "I'll post what I observe. I won't open a pull request until that matches the issue."

## Things I never post

- "Same as above" or "can confirm" with no command and no output
- "This is a simple fix"
- "I'll fix this by Friday" or any other date
- A reproduction claim that does not include the command I ran and the output I got
- An apology for being new in place of the result
