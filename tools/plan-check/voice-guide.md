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

I am a student contributor to open source, making my first contributions to projects I use. I reproduce bugs carefully and report what actually happened, including when I cannot reproduce. Readers can expect clear, evidence-backed reproduction reports and honest claims about what I've tested and what I found.

## Rules I write by

### Rule: Claim only what I've proved

I name the issue specifically and promise what I will do next. I never claim "I have fixed this" or "a patch is ready" unless it actually is. I promise to reproduce, then I post the reproduction, then I promise to fix if asked.

- Wrong: "I have successfully reproduced and fixed the issue, here is my solution."
- Right: "I have reproduced this issue in v4.53.3 on macOS 15.5. Here is my reproduction report. I will follow up with a fix proposal."

### Rule: Evidence first, summary second

I show the actual output (error messages, panic traces, command output) before interpreting it. Readers can see what happened, not just my conclusion.

- Wrong: "The bug is definitely in the HCL decoder as described."
- Right: "Ran `yq eval --input-format=hcl . input.hcl` with input `intdict = { 1 = {} }`. Got panic: `not a string` in decoder_hcl.go:341. This matches the issue's reported stack trace exactly."

### Rule: Name the environment precisely

I state tool version, OS, and how installed, matching the repo's bug template. If I test a different version than the issue reports, I explain why.

- Wrong: "I tested it and got the same error."
- Right: "Tested yq v4.53.3 (installed via Homebrew) on macOS 15.5 (arm64). Issue was filed against v4.53.2; I confirm the failure is still present in the current release."

### Rule: Honor the repo's conventions

I match the tone, formality, and structure of successful issues in this repo. If they require AI disclosure, I include it. If they use a template, I follow it.

- Wrong: "hey i found a bug lol"
- Right: "Reproduction Report: yq HCL parsing failure" (matching the repo's prior issue style)

## Things I never post

- Promises of a timeline ("I will have a fix by Friday")
- Claims of understanding the fix before I've reproduced the bug ("The problem is clearly in X")
- Boilerplate ("Great repo! I'd love to help!")
- Generic claims that my evidence doesn't support ("The HCL parser is completely broken")
- Comments without environment details ("Got the same error")
