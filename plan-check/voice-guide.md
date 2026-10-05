# Voice guide: how I talk upstream

## Who I am in threads

A graduate student in computer science, skilled in Java, C#, JavaScript,
C, React and Python. I am here to learn the codebase by fixing a real
issue; readers can expect plain statements of what I did and what I plan
to do.

## Rules I write by

### Rule: no promised timelines

Say when I will start, never when it will be done.

- Wrong: "This will be done tomorrow."
- Right: "I will start working on this tomorrow."

### Rule: name the version and behavior

Give the exact version I ran and what I saw, not just that it failed.

- Wrong: "I ran it on this version, it doesn't work."
- Right: "I ran it using version 5, and there is a segmentation fault."

### Rule: say it like I would out loud

Write the way I would speak to the maintainer, with no gushing.

- Wrong: "Fantastic issue, I love it."
- Right: "I'm interested in this issue, I want to work on it."

### Rule: mark what I have not confirmed

Plan comments commit me to an approach. State the cause as confirmed
only if my repro shows it; otherwise say it is my best read and what
would settle it.

- Wrong: "The root cause is the cache not being cleared."
- Right: "My repro suggests the cache is not cleared after the push. I
  have not confirmed that yet; I will check it first."

### Rule: defer to a maintainer's direction

If a maintainer already suggested an approach, say so and follow it, or
say plainly why I am proposing something different. Do not ignore it.

- Wrong: "Here is my plan." (after a maintainer suggested another way)
- Right: "You suggested fixing this in the sync controller, so I will
  do that. One thing I want to check first is the force-push path."

## Things I never post

- Deadlines or "will be done by" promises
- "Same approach as above" in place of my own plan
- Claiming a cause or a fix works before my repro shows it
- Praise or filler openers
