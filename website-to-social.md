---
name: website-to-social
description: Turn a webpage or blog post URL into ready-to-post social copy — an X/Twitter post, a LinkedIn post, a Facebook post, and a short plain-text excerpt (the kind that goes in a WordPress excerpt or meta description field). Use this whenever the user shares a URL and asks for social posts, promo copy, "posts for this article", "share this on socials", an excerpt or meta description, or anything about promoting a published page — even if they only paste a link with a word like "socials", "promote this", or "write posts". Also use when they ask for just one of those four formats from a URL.
---

# Website to Social

Read a page, understand what it actually says, and write four pieces of copy the user can paste straight into their posting tools.

## Workflow

1. **Get the URL.** If none was provided, ask for it and stop. Never write posts from a topic guess.
2. **Fetch the page** with `web_fetch`. If the fetch fails or returns almost nothing (paywall, JS-rendered page, cookie wall), say so plainly and ask the user to paste the text instead. Do not fill the gap with plausible-sounding invention.
3. **Read for substance**: what the piece argues or announces, who it's for, the two or three details a reader would actually care about, and the single most surprising or useful line in it.
4. **Decide the voice** (see below).
5. **Write the four pieces** and return them inline in chat, using the output template.

## Deciding the voice

The user promotes a mix of their own work and other people's, so infer per URL rather than defaulting:

- **First person** ("I wrote about…", "New post on…") when the user says it's theirs — "my post", "I published", "we shipped" — or the byline or domain matches a site they've identified as theirs earlier in the conversation.
- **Neutral sharing** ("A good breakdown of…", "This post explains…") for anyone else's content. Neutral still means warm and specific, just never implying authorship.
- If it's genuinely ambiguous and the framing would change the copy, ask one short question before writing. Don't ask if the answer doesn't change much — when in doubt, write neutral, since falsely claiming authorship is the worse error.

## Format specs

### X / Twitter
- Hard ceiling 280 characters. **Target 240–255** so the user can append the link — X counts any URL as 23 characters regardless of length.
- Do not paste the URL into the draft; they'll add it when posting.
- One idea, stated concretely. Lead with the substance, not "Check out my new post about…".
- 2–3 hashtags, at the end.
- Emojis only if one genuinely earns its place. Default to none.

### LinkedIn
- 2–3 short paragraphs, one to three sentences each, with blank lines between them — LinkedIn truncates after roughly 200 characters, so the first line has to carry the hook on its own.
- Professional but human. No hashtags unless the user asks.
- Make the takeaway explicit: what a reader gets from this, or what changes if they act on it.
- End with a real question or a clear call to action.

### Facebook
- Conversational, the way you'd tell a colleague about it. Short paragraphs, generous line breaks.
- Invite discussion — a question tied to the reader's own experience beats "Thoughts?".
- 2–3 hashtags at the end.

### Excerpt
- 200 characters maximum, plain text, one or two sentences.
- No hashtags, no emojis, no links, no line breaks.
- Descriptive, not promotional. It should tell a reader what the page covers so they can decide whether to click.
- Avoid marketing register entirely: no "discover", "unlock", "game-changing", "must-read", "everything you need to know", no exclamation marks.

**Example (post about fixing slow WordPress queries):**
- Weak: `Discover the game-changing tricks that will supercharge your WordPress site!`
- Good: `How unindexed postmeta queries slow down WordPress admin screens, and three ways to profile and fix them without a caching plugin.`

## Writing quality

The failure mode here is four posts that sound like a press release for a page nobody read. To avoid it:

- Use a specific detail from the article — a number, a named tool, the actual claim — in at least the X and LinkedIn posts. Specificity is what makes copy sound like a person.
- Don't reuse the same sentence across platforms. Each format has a different reader and rhythm.
- Cut hype adjectives, "in today's fast-paced world", "dive into", "it's not just X, it's Y", and rhetorical questions used as openers.
- Hashtags should be ones people actually follow or search (`#WordPress`, `#WebPerf`), not filler like `#blog` or `#content`. CamelCase multi-word tags for screen readers: `#WebPerformance`.
- Never state a fact, statistic, or quote that isn't in the source page.
- Paraphrase rather than quoting. If an exact phrase is essential, keep it under 15 words and in quotation marks.

## Output template

Return exactly this, with real character counts you have actually verified:

```
**X / Twitter** (247 characters)
[post]

**LinkedIn**
[post]

**Facebook**
[post]

**Excerpt** (186 characters)
[excerpt]
```

Count characters carefully rather than estimating — if the X post lands over 255 or the excerpt over 200, rewrite it before responding, don't ship it with an apology. Add no preamble or commentary beyond a single line if something genuinely needs flagging (e.g. the page was thin, or the voice call was a guess).

If the user asks for only one format, give just that one, same rules.
