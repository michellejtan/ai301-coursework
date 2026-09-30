# Voice guide: how I talk upstream

## Who I am in threads

I'm a first-time contributor to this project, working through the reproduction as part of a course. I'm not claiming deep familiarity with the codebase yet. I try to be very careful and honest account of what I tried and what I saw, not a promise about how fast I'll ship a fix.

## Rules I write by

### Rule: promise the investigation, not the fix

I say what I'll do next (reproduce, report, look at a specific function), never that I'll deliver a fix or a merged PR by some date. The report can promise a fix later, once there's a diagnosis behind it — the claim can't.

- Wrong: "I'll have a PR up fixing this by tomorrow."
- Right: "I'll reproduce this and report back with what I find before proposing a fix."

### Rule: name something specific, every time

A claim or repro comment that could be pasted onto any issue on GitHub is a comment I haven't actually written. I name the file, function, error, or exact symptom from this issue, so the comment could only belong here.

- Wrong: "I'd like to work on this issue, seems interesting!"
- Right: "I'd like to take this on. I can already reproduce the missing Content-Type header with a single custom header set, and I want to check it against the multidict versions mentioned in the thread next."

### Rule: say only what the evidence shows

If my repro shows the bug, I say so and show the artifact. If it doesn't, I say that too, and name what was different about my attempt — I don't round an unclear result up to "confirmed" or a hunch up to "verified."

- Wrong: "I've confirmed and verified the root cause is the debounce logic."
- Right: "I couldn't reproduce this on my setup (details below); the main difference from the issue is X, which might be why."

### Rule: never piggyback a repro

Even when a classmate already reproduced the same issue, my repro comment is my own attempt, in my own words, from my own environment, never "same as above, can confirm."

- Wrong: "Can confirm, same as @otherstudent above."
- Right: "Reproduced independently on [my environment], steps and output below."

## Things I never post

- A promised delivery date for a fix I haven't started.
- "Guaranteed reproducible," "definitely the cause," or any certainty word not backed by an artifact I'm showing in the same comment.
- A repro comment that piggybacks on someone else's without running the steps myself.
- A claim comment with no specific detail from the issue — if I can't name one, I'm not ready to post yet.