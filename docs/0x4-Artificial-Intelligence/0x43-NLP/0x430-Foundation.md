# 0x430-Foundation

- [1. Historical Lingustics](#1-historical-lingustics)
    - [1.1. Language Family](#11-language-family)
        - [1.1.1. Indo-European (Derived from PIE)](#111-indo-european-derived-from-pie)
        - [1.1.2. Sino-Tibetan](#112-sino-tibetan)
        - [1.1.3. Niger-Congo](#113-niger-congo)
        - [1.1.4. Afro-Asiatic](#114-afro-asiatic)
        - [1.1.5. Austronesian](#115-austronesian)
- [2. Character Encoding](#2-character-encoding)
    - [2.1. ASCII](#21-ascii)
    - [2.2. Unicode](#22-unicode)
        - [2.2.1. UTF-8](#221-utf-8)
        - [2.2.2. UTF-16](#222-utf-16)
        - [2.2.3. UTF-32](#223-utf-32)
- [3. Reference](#3-reference)

## 1. Historical Lingustics
Historical linguistics studies how languages change in time and space

*   **Diachrony**: study development and evolution of languages through time
*   **Synchrony**: study language at a moment in time

### 1.1. Language Family

#### 1.1.1. Indo-European (Derived from PIE)

*   Germanic: English, German (Grimm's law)
*   Romance: Italic, French, Spanish(Derived from Vulgar Latin)
*   Hellenic: Greek
*   Balto-Slavic: Russian, Czech, Polish
*   Indo-Iranian: Hindi, Bengali
*   Celtic: Welsh (VSO)

#### 1.1.2. Sino-Tibetan

*   Chinese, Tibetan languages

#### 1.1.3. Niger-Congo

The largest language family by the number of languages (~1500), 3rd largest family by the number of speakers (~700m)

*   Bantu: swahili, zulu
*   Yoruba
*   Igbo

#### 1.1.4. Afro-Asiatic

*   Arabic (VOS), Hebrew (VOS), Aramaic

#### 1.1.5. Austronesian

*   Verb initial (VOS)
*   Malay, Indonesian, Walpiri, Malagacy

## 2. Character Encoding

### 2.1. ASCII

### 2.2. Unicode
Unicode is a character set where each character (called code point) is assigned an id from U+000000 ~ U+10ffff.

The set can be divided into 17 planes. Each planes contains 2 bytes (U+0000 ~ U+ffff). There are 17 planes because (U+00xxxx ~ U+10xxxx)


**Plane 0 BMP (Basic Multilingual Plane)**
The first planes contains character U+0000 - U+FFFF

**Plane 1~16 (Supplementary Plane)**
Notice there are unsigned planes (plane 4~13) and several private planes (plane 15, 16)


Unicode only assigns the code point to each character, however, it does not state how to encode those code points. UTF-8, 16, 32 are just different encoding scheme (implementation) of Unicode.

#### 2.2.1. UTF-8
Variable-length encoding, **backwards compatible with ASCII**, will not be affected by endianness
Good for English, 96.0\% of all  web pages as of 2021 according to Wikipedia. It is recommended from the WHATTWG for HTML and DOM spec.

Encoding is done as follows:
- U+0000 - U+007F: 1 byte (ASCII) 0xxxxxxx
- U+0080 - U+07FF: 2 bytes 110xxxxx 10xxxxxx
- U+0800 - U+FFFF: 3 bytes 1110xxxx 10xxxxxx 10xxxxxx
- U+10000 - U+10FFFF: 4 bytes 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx

#### 2.2.2. UTF-16
Variable-length encoding, either 2 byte or 4 byte. Has different endianness
Good for Asian texts, Bad for English

- U+000000 - U+00ffff: 2 byte (xxxxxxxx xxxxxxxx)
- U+010000 - U10fffff: 4 byte (110110yy yyyyyyyy 110111xx xxxxxxxx)

The 4 byte is to use encode code points in supplementary planes.
- The first part (110110yy yyyyyyyy) is called the high surrogate, with hex (0xD800 - 0xDBFF)
- The second part (110111xx xxxxxxxx) is called the low surrogate, with hex (0xDC00 - 0xDFFF)

If all xy are 0, then it is U+0x010000. if all 1, it is 0x10ffff


#### 2.2.3. UTF-32
Fixed-length encoding, all code points take 4 bytes. Has different endianness
Fast to operate (because of fixed length) but rarely used due to the waste of memory.

## 3. Reference