---
name: thai-transcribe
description: Transcribe Thai text to Roman alphabet using Royal Institute of Thailand's 1999 transcription rules. Use when the user asks to convert Romanize, or transliterate Thai text.
user-invocable: true
allowed-tools:
  - Read
  - Write
---

# /thai-transcribe — Thai to Roman Alphabet (Royal Institute System)

Transcribe Thai text into Roman alphabet using the Royal Institute of Thailand's 1999 transcription-by-pronunciation rules.

Arguments passed: `$ARGUMENTS`

---

## How to use

When the user provides Thai text, transcribe it syllable by syllable using the rules below. Output the final Romanized result as a single string, then optionally show a breakdown table.

Example:
- Input: `สวัสดีครับ`
- Output: `sawatdi khrap`

---

## 1. Consonant Mapping

### Initial position (start of syllable)

| Thai | Roman | Thai | Roman |
|------|-------|------|-------|
| ก, ข, ฃ, ค, ฅ, ฆ | k | จ, ฉ, ช, ฌ | ch |
| ง | ng | ซ, ศ, ษ, ส, ทร | s |
| ต, ฏ, ฐ, ฑ, ฒ, ถ, ท, ธ | th | ฎ, ฑ (sound d) | d |
| ตา (regular ด) | d | ฐ, ฑ (sound th), ถ, ท, ธ | th |
| น | n | บ, ป | b |
| ผ, พ, ภ | ph | ฝ, ฟ | f |
| ม | m | ย | y |
| ร | r | ล, ฬ | l |
| ห, ฮ | h | ว | w |
| แกะ (ย as vowel glide) | - | นน (ฯ) | see §4 |

### Final position (end of syllable)

| Thai | Roman | Notes |
|------|-------|-------|
| ก, ข, ฃ, ค, ฅ, ฆ, ด, ต, ฎ, ฏ, จ, ช, ซ, ฏ | t | Stop consonants |
| ง | ng | |
| บ, ป | p | |
| ผ, พ, ภ | p | |
| ม | m | |
| น | n | |
| ล, ฬ | n | Often becomes n at syllable end |
| ร | n | |
| ห, ฮ, ว | (silent) | Glottal stop, not transcribed |

**Key rule:** Stop consonants (ก, จ, ต, ป, etc.) always map to `t` or `p` at final position regardless of their initial mapping.

---

## 2. Vowel Mapping

| Thai | Roman | Thai | Roman |
|------|-------|------|-------|
| อะ, -ั, อา, รร | a | อิ, อี | i |
| อึ, อื | ue | อุ, อู | u |
| เอะ, เ-็, เอ | e | แอะ, แอ | ae |
| โอะ, -โ- (reduce), โอ, เอาะ, ออ | o | เอะ, เ-ิ, เออ | oe |
| เอียะ, เอีย | ia | เอือะ, เอือ | uea |
| อัวะ, อัว, -ว- | ua | ใอ, ไอ, อัย, ไอย, อาย | ai |
| เอา, อาว | ao | อุย | ui |
| โอย, ออย | oi | เอย | oe |
| เอือย | ueai | อวย | uai |
| อิว | io | เ็ว, เว | eo |
| แอ็ว, แอว | aeo | เอียว | iao |
| ฤ (rue), ฤๅ | rue | ฤ (ri) | ri |
| ฤ (roe) | roe | ภ, ภๅ | lue |

---

## 3. Processing Steps

1. **Tokenize** the Thai sentence into words.
2. **Split each word into phonetic syllables** (G2P). This requires knowing the pronunciation, not just the spelling.
3. **Map each syllable** using the consonant tables (initial + final) and vowel table.
4. **Apply formatting rules** (§4 below).
5. **Output** the result.

---

## 4. Formatting Rules

### Spacing
- Separate words by spaces.
- Compound words and names: keep together without spaces (e.g., `ลูกเสือ` = `luksuea`, not `luk suea`).

### Hyphenation (syllable boundary ambiguity)
- Previous syllable ends in vowel, next starts with `ng` (ง): `สง่า` = `sa-nga`
- Previous ends in `ng` (ง), next starts with vowel: `บังอร` = `bang-on`
- Syllable starts with vowel sound: `สะอาด` = `sa-a-at`, `สำอาง` = `sam-ang`

### Capitalization
- Capitalize first letter of proper nouns (names, places, organizations).
- Capitalize titles when part of a proper name: `นายปรีดา` = `Prida` (title implied, context-dependent).
- Capitalize first word of a paragraph.

### Geographical names
- Keep the common noun portion transcribed, not translated: `ถนนท่าพระ` = `Thanon Tha Phra` (not "Tha Phra Road").

### Loanwords
- Independent proper nouns: keep original English spelling.
- Part of Thai proper noun: transcribe per Thai pronunciation rules.

---

## 5. Special Characters & Symbols

| Thai | Handling | Example |
|------|----------|---------|
| ๆ (Mai Yamok) | Duplicate preceding word's transcription | `ทำบ่อย ๆ` = `tham boi boi` |
| ฯ (Paiyan Noi) | Expand to full known word | `กรุงเทพฯ` = `Krung Thep Maha Nakhon` |
| ฯลฯ (Paiyan Yai) | End of sentence: `lae uen uen`; middle (up to): `la thueng` |
| พน. (Phanathan) | `phanathan` |
| Abbreviations | Transcribe full pronunciation | `จ.` = `changwat`, `ชม.` = `chuamong` |

---

## 6. Numbers

Convert numbers to Thai phonetic equivalents:

| Number | Thai phonetic |
|--------|--------------|
| 0 | zero / sut |
| 1 | nueng |
| 2 | song |
| 3 | song sam |
| 4 | si |
| 5 | ha |
| 6 | hoe |
| 7 | et |
| 8 | paet |
| 9 | kao |

Examples:
- `4.50 บาท` = `si bat ha sip satang`
- `1000` = `nueng phan`
- `05.00 น.` = `ha nalika`

---

## 7. Common Words Reference

| Thai | Transcription | Notes |
|------|--------------|-------|
| สวัสดี | sawatdi | |
| ครับ (male speaker) | khrap | |
| ค่ะ (female speaker) | kha | |
| ผม (male "I") | phom | |
| ข้าน้อย / ฉัน (female "I") | chan | |
| คุณ (you) | khun | |
| ชื่อ | chue | |
| คือ | kue | |
| ใช่ | chai | |
| ไม่ | mai | |
| ได้ | dai | |
| ไป | pai | |
| มา | ma | |
| ที่ | thi | |
| นี้ | ni | |
| นั้น | nan | |
| ของ | khang | |
| คน | khon | |
| มาก | mak | |
| ครับ (polite particle) | khrap / kha | |

---

## 8. Important Warnings

1. **Spelling ≠ Pronunciation**: Many Thai words are spelled differently from how they're pronounced. Examples:
   - `ดี` (spelled di) is pronounced `di` but `ด` as final consonant is `t` → `det` in final position
   - `สิบ` would be pronounced `sip` not `sib`
   - `สวัสดี` → `sawatdi` (the spelling has extra consonants not pronounced)

2. **G2P is required**: A pure character-by-character mapping will fail on many words. A pronunciation dictionary or G2P engine is needed for accurate transcription.

3. **Stop consonants at syllable end**: Always map to `t` or `p` regardless of their initial position mapping.

4. **Compound words**: Be careful with word boundaries. `ลูกเสือ` is one word (`luksuea`), not two (`luk suea`).

---

## Example Walkthrough

Input: `สวัสดีครับ ผมชื่อสมชาย`

Step 1 - Tokenize: `สวัสดีครับ` | `ผม` | `ชื่อ` | `สมชาย`

Step 2 - G2P syllables:
- `สวัสดีครับ` → `sa-wat-di-khrap`
- `ผม` → `phom`
- `ชื่อ` → `chue`
- `สมชาย` → `som-chai`

Step 3 - Map each syllable:
- `sa` → s + a
- `wat` → w + a + t
- `di` → d + i
- `khrap` → kh + r + a + p
- `phom` → ph + o + m
- `chue` → ch + u + e
- `som` → s + o + m
- `chai` → ch + a + i

Step 4 - Join: `sawatdi khrap phom chue somchai`

Final output: `sawatdi khrap phom chue somchai`
