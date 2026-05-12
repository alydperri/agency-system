# Voice Profiles

## What This Is

The `03_client_communication` specialist drafts in the agent's voice. For that to work, it needs to know more than writing style — it needs to know how each agent thinks about client communication: what they lead with, what they avoid, and when they'd pick up the phone instead of sending a text.

That's what a voice profile captures.

## What Goes In a Profile

Each profile has four sections:

**1. Communication defaults**
How this agent naturally operates. How direct are they? How much context do they give before getting to the point? Do they check in proactively or wait until there's something to report? This is the behavioral layer underneath the writing.

**2. Sample messages**
3–5 real messages this agent has sent to clients. Paste them in as-is — don't edit for quality. The specialist needs to see how they actually write, not how they wish they wrote. Texts and emails both useful; include both if you have them.

**3. What they never do**
Language, habits, or approaches this agent actively avoids. This is as important as the samples — it's the negative space of their voice.

**4. When they call instead of write**
Every agent has a threshold where text or email isn't enough. Knowing that threshold keeps drafts from being sent into situations where the agent would actually pick up the phone.

## How to Create a Profile

Copy `TEMPLATE_voice.md` and rename it to the agent's first name (e.g. `marcus.md`). Fill it out in one sitting — it takes about 15 minutes. The quality of communication drafts depends directly on the quality of this file.

Profiles are for internal use only. Do not commit real client messages to a public repo — keep voice files private or git-ignored if your repo is public.

## How the Specialist Uses It

When `03_client_communication` receives a handoff, it loads the named agent's voice profile before drafting. If no profile exists for that agent, it will not draft — it will ask for one first.

A draft produced without a voice profile is a generic draft. Generic drafts don't pass quality review.

## Keeping Profiles Current

Update a profile when an agent's communication style shifts noticeably — after a particularly good stretch of client feedback, after they've been on the team long enough to develop a more distinct voice, or when they explicitly say "I wouldn't say it that way."

Profiles don't need to be perfect on day one. A working profile is better than a perfect profile that hasn't been written yet.
