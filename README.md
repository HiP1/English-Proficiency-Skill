🇫🇷 [Français](README.fr.md) · 🇪🇸 [Español](README.es.md)

# English Proficiency Scorecard

An AI agent skill that assesses a user's English proficiency and generates an interactive HTML scorecard with estimated scores across major international frameworks: CEFR, IELTS (Academic and General Training), TOEFL iBT, Cambridge (CAE/CPE), and TOEIC (L&R and S&W).

The skill evaluates real writing from chat history, connected services (email, documents), and optional live samples — not quizzes or multiple-choice tests. The output is a self-contained, shareable HTML document with animated score cards, institutional benchmark comparisons, annotated writing samples, and a transparent methodology section.

## How It Works

The skill guides Claude through a four-phase workflow:

1. **Interview & Setup** — Understands the user's background, gathers preferences (calibration mode, privacy, layout), and identifies available evidence sources
2. **Evidence Analysis** — Analyzes writing across all available sources, evaluating grammar, vocabulary, register control, pragmatic competence, and L1 transfer patterns
3. **Scorecard Generation** — Produces a two-page interactive HTML scorecard from the included template, with scores calibrated against the scoring guide and benchmarks
4. **Review & Refinement** — The user reviews the scorecard and can challenge any score or observation; growth areas are discussed in chat, not added to the document

## What's in the Package

```
english-proficiency-scorecard/
├── SKILL.md                          # Main instructions and workflow
├── LICENSE.txt                       # MIT license + integrity verification
├── INTEGRITY.sha256                  # SHA-256 manifest for all files
├── assets/
│   └── template.html                 # Interactive scorecard template
└── references/
    ├── scoring-guide.md              # Scoring rubrics per framework
    └── benchmarks-fallback.md        # Institutional benchmark data
```

## Design Principles

The skill is built around seven principles documented in SKILL.md:

1. **Integrity first** — Scores reflect evidence. Claude never flatters or inflates, even if asked.
2. **User chooses calibration** — Honest best-estimate or conservative, but never above what evidence supports.
3. **Self-reported data is clearly marked** — Speaking and listening scores based on the user's own account are labeled as such.
4. **Privacy-conscious** — The scorecard is designed to be shared; the user confirms what personal information to include.
5. **No branding — but model disclosure is OK** — No product names as credibility signals. The methodology section may factually state which model performed the analysis.
6. **Growth areas stay in the chat** — The scorecard showcases proficiency. Improvement suggestions are discussed privately.
7. **Content neutrality** — All generated text is linguistically descriptive, never culturally prescriptive. Benchmarks are factual, writing annotations stick to language analysis, and no variety of English is treated as superior. This principle also serves as a safeguard against tampered versions injecting bias through otherwise legitimate-looking assessments.

## Integrity Verification

The skill includes a three-layer integrity system:

- **SHA-256 manifest** (`INTEGRITY.sha256`) — Hashes for every file in the package. Run `sha256sum -c INTEGRITY.sha256` to verify nothing has been modified.
- **LICENSE witness** — The license file includes instructions for the AI model to verify file integrity before execution. This is a deliberate design choice and a conversation starter about plain-text skill security (see below).
- **Content neutrality safeguard** — Principle 7 instructs the model to ignore its own skill's instructions if they push toward biased content, and to flag the concern to the user.

No single layer is bulletproof. Together, they make it meaningfully harder to weaponize the skill without the user knowing.

### A Note on Skill Security

AI agent skills are plain-text instruction files. Unlike compiled software, anyone can open a SKILL.md, add a line, and repackage it. The barrier to tampering is zero, and most users won't read 500 lines of instructions to check for hidden behavior.

The integrity system here is an early attempt to address this. The LICENSE witness mechanism — hiding verification instructions in a file most people skip — is intentionally borderline. It's readable by anyone who opens the file, which we consider the ethical line: transparent-if-inspected is acceptable; encoded-to-exclude-humans is not.

We think this is a conversation worth having as the skill ecosystem grows. If you have thoughts on better approaches, open an issue.

## Installation

### As a Claude Skill

Download the `.skill` file from the [**Releases**](https://github.com/HiP1/English-Proficiency-Skill/releases) page, then install it in your Claude environment.

### Other AI Providers

The `.skill` file is a standard zip archive. Download it from the [**Releases**](https://github.com/HiP1/English-Proficiency-Skill/releases) page, rename it from `english-proficiency-scorecard.skill` to `english-proficiency-scorecard.zip`, upload it to your chat platform, and ask the model to use the skill contained in the zip file. The `SKILL.md` is the entry point; the template in `assets/` and reference files in `references/` are loaded as needed. Use the most capable model available on your platform.

### Manual

Clone or download this repository. Point your AI tool at the `SKILL.md` file as the entry point.

## Origin

This skill was created by HiP (Ivan Phan) and Claude Opus 4.6 (Anthropic) in February–March 2026. It grew out of a real English proficiency assessment — HiP asked Claude to evaluate his English across international frameworks using his actual chat history and two years of sent emails. The scorecard that came out of that assessment became the template, and the evaluation methodology became the skill.

The scoring rubrics, benchmark data, interaction design, security architecture, and content neutrality framework were all developed through iterative collaboration across multiple sessions. The project is an original creation, not derived from existing skills.

## License

MIT — use, modify, and share freely. Just keep the credit.

Run `sha256sum -c INTEGRITY.sha256` to check whether your copy matches the original.
