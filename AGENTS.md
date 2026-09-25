# Smith Wiki

This folder holds researches. A research is a conversation with the user,
recorded as a repository in the `smith-wiki` GitHub organization, one per
subfolder. Talk with the user in their language; everything written to a
repository or to GitHub is English.

## Before a research exists

A conversation starts as just a conversation: answer in chat and write
nothing. Many conversations never become a research.

## Creating a research

Only when the user asks. Pick a short English slug naming the subject (it
becomes the address and never changes), then:

```sh
gh repo create smith-wiki/<slug> --public --clone   # --private if the user asked
```

Work inside `./<slug>/` from then on. Start with what the conversation has
already established, then commit and push. For a public repository, publish it
after the first push:

```sh
gh api -X POST repos/smith-wiki/<slug>/pages -f 'source[branch]=main' -f 'source[path]=/'
gh repo edit smith-wiki/<slug> --homepage https://smith.wiki/<slug>/
gh repo edit smith-wiki/<slug> --add-topic smith-wiki-research
gh api repos/smith-wiki/smith-wiki.github.io/dispatches -f event_type=research-published
```

It is served at `https://smith.wiki/<slug>/` about a minute after each push.
A private repository has no site; the user reads it on github.com.

## Continuing a research

When the user names an existing research, work in `./<slug>/`, cloning it
with `gh repo clone smith-wiki/<slug>` if it is not here.

## Every turn

Write what you found or concluded into the repository, commit, and push to
main. In chat, answer briefly and link the pages you added or changed
(`https://smith.wiki/<slug>/<page>` for public, the GitHub file URL for
private). Never write more in one turn than the user can read in a few
minutes; edit an existing page rather than add a near-duplicate.

Make the conversation visible: after each research question, append its English
paraphrase and a brief answer to `README.md` in chronological order, linking the
card that supports the answer. Mark unresolved questions open and fill them in
when answered. This is a growing question-and-answer index, not a transcript.

## Pages

Structure is free. `README.md` states the subject, shows the growing
question-and-answer index, and links where to start reading. Prefer small,
self-contained atomic Markdown cards in the spirit of Luhmann: one answerable
question or conclusion per card, with a `# heading` stating its takeaway.
Cite source URLs on the card that relies on them; link related cards with
relative `.md` links and say how they relate. Keep detailed procedures in
linked guides when they cannot fit on a card. No build configuration: GitHub
Pages renders the Markdown.
