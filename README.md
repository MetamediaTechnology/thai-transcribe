# /thai-transcribe — Thai Transcription Skill for Claude Code

Transcribe Thai text to Roman alphabet using the **Royal Institute of Thailand's 1999 transcription rules**. Pronunciation-based, not character-by-character.

## Example

| Thai | Transcription |
|------|--------------|
| สวัสดีครับ | `sawatdi khrap` |
| ผมชื่อสมชาย | `phom chue somchai` |
| ไปเจอกันที่สุขุมวิท | `pai joe kan thi sukhumwit` |

## Installation

### Install to all projects (global)

```bash
# From this repo (after cloning or downloading):
mkdir -p ~/.claude/skills
cp -r .claude/skills/thai-transcribe ~/.claude/skills/thai-transcribe
```

### Install to a single project

```bash
# In your project root:
mkdir -p .claude/skills
cp -r path/to/thai-transcribe/.claude/skills/thai-transcribe .claude/skills/
```

Then restart Claude Code.

## Usage

In Claude Code, type `/thai-transcribe` followed by Thai text:

```
/thai-transcribe สวัสดีครับ ผมชื่อสมชาย
```

Or just ask Claude Code to transcribe Thai text directly — the skill auto-activates.

## What's Inside

- `SKILL.md` — The complete skill definition with all transcription rules
- `README.md` — This file
- `LICENSE` — MIT License

## Rules Covered

- Consonant mapping (initial & final position)
- Vowel & diphthong mapping
- Spacing, hyphenation & capitalization rules
- Special characters (ๆ, ฯ, ฯลฯ)
- Number-to-phonetic conversion
- Common words reference table

## License

MIT — see [LICENSE](LICENSE) file.
