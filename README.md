# MinnaNoDS
<p align="center">
  <a href="https://yaml.org/">
    <img alt="YouTube" src="https://img.shields.io/badge/YAML-CB171E?logo=yaml&logoColor=fff&style=flat-square"
  /></a>
  <a href="https://en.wikipedia.org/wiki/Japanese_language">
    <img alt="Python" src="https://img.shields.io/badge/lang-%20%E6%97%A5%E6%9C%AC%E8%AA%9E-forestgreen?style=flat-square"
  /></a>
  <a href="https://github.com/vitto4/MinnaNoDS/releases">
    <img alt="GitHub Release" src="https://img.shields.io/github/v/release/vitto4/MinnaNoDS?style=flat-square"
  /></a>
  

</p>

<p align="center">All of the vocabulary from your <code>Minna no Nihongo Shokyū Ⅰ & Ⅱ</code> textbooks formulated into a tiny little YAML file.</p>

<br>


```yaml
  - id: [2, 10]
    edition: [1, 2]
    kanji: "新聞"
    kana: "しんぶん"
    romaji: "shinbun"
    meaning: {
      en: "newspaper",
      fr: "journal",
    }
```
<p align="center"><sup><ins><i>Figure</i></ins> – A word straight from the dataset. More information on the format <a href="https://github.com/vitto4/MinnaNoDS/blob/ae20b1408e2752642618312728ff817fe2479dd4/minna-no-ds.yaml#L93-L107">this way</a>.</sup></p>



## 🧭 Table of contents
1. [Overview](#-overview)
1. [Usage](#️-usage)
1. [Bibliography](#-bibliography)
1. [Conventions](#-conventions)
1. [Notes](#-notes)
1. [Warning](#-warning)

## ☁ Overview

This project aims to serve as a comprehensive vocabulary list for the [`Minna no Nihongo Shokyū`](https://www.3anet.co.jp/np/en/list.html?af=1&g=7-12-33&s=1 "みんなの日本語 初級 Ⅰ & Ⅱ") series, packaged into a single YAML file – which we'll refer to as *the dataset*. <br>
To be more specific, it intends to be as close as possible to the source material, in an effort to (hopefully) provide a foundation anyone can use or expand on.


This fork adds two things on top of [vitto4/MinnaNoDS](https://github.com/vitto4/MinnaNoDS):

- a reviewed **`norm` block** on every entry: dictionary-form headword, reading, card display, POS and kind. See [`CONVENTIONS.md`](CONVENTIONS.md#-the-norm-block-normalised-headwords).
- **`minna-no-ds-intermediate.yaml`**, with the vocabulary of *Minna no Nihongo Chūkyū* in the same format (English meanings only, `edition: [3]`).

The dataset currently targets two languages for `meaning` :
```yaml
languages:
  en: "English"
  fr: "Français"
```
<p align="center"><sup> Further information <a href="https://github.com/vitto4/MinnaNoDS/blob/ae20b1408e2752642618312728ff817fe2479dd4/minna-no-ds.yaml#L26-L31">here</a>.</sup></p>


**Rōmaji** are provided solely for convenience, and do not correspond to those of the [*rōmaji edition*](https://www.3anet.co.jp/np/en/books/2303/ "みんなの日本語 初級 ローマ字版") of the books. <br>
These were generated using a mix of [`pykakasi`](https://pypi.org/project/pykakasi/) and readings supplied by [Google Translate](https://translate.google.com/). As a result, they more or less follow standards set by the [*Modified Hepburn*](https://en.wikipedia.org/wiki/Hepburn_romanization#Variants) system (yes, mācrōns inclūdēd !).

## ⚙️ Usage

Here is a basic example in [`python`](https://www.python.org/).

```py
import yaml

# Load the dataset
with open("minna-no-ds.yaml", "r", encoding="utf-8") as f:
  ds = yaml.load(f, Loader=yaml.FullLoader)


# Extract the keys for all available lessons
lessons: list = [lesson["key"] for lesson in ds["lessons"]] # ['lesson-01', 'lesson-02', ...]


# Go through each lesson and print out its contents
for key in lessons:
  print(f"Contents of {key}") # Outputs : Contents of lesson-01
  print(ds[key]) # Outputs : [{'id': [1, 1], 'edition': [1, 2], 'kanji': None, 'kana': 'わたし', 'romaji': 'watashi', 'meaning': {'en': 'I', 'fr': 'je, moi'}}, ...]
```

## 📚 Bibliography

As you may know, `Minna no Nihongo Shokyū` comes in two books of twenty-five lessons each ; both available in two editions (the second of which is an updated version of the original).

Presented bellow is a table showing the books used in the making of the dataset.

| 📗📘📙 | First Edition | Second Edition |
|:-----:|:-------------:|:--------------:|
| **Book 1**<br>*English Version*  | みんなの日本語初級Ⅰ 翻訳・文法解説英語版<br>[`ISBN : 9784883191079`](https://web.archive.org/web/20040820203739/http://www.3anet.co.jp/english/text_e_m_trans.html) | みんなの日本語初級Ⅰ 第２版 翻訳・文法解説 英語版<br>[`ISBN : 9784883196043`](https://www.3anet.co.jp/np/en/books/2302/) |
| **Book 2**<br>*English Version* | みんなの日本語初級Ⅱ 翻訳・文法解説英語版<br>[`ISBN : 9784883191086`](https://web.archive.org/web/20040820203739/http://www.3anet.co.jp/english/text_e_m_trans.html) | みんなの日本語初級Ⅱ 第２版 翻訳・文法解説 英語版<br>[`ISBN : 9784883196647`](https://www.3anet.co.jp/np/en/books/2402/) |
| **Book 1**<br>*French Version*  | みんなの日本語初級Ⅰ 翻訳・文法解説フランス語版<br>[`ISBN : 9784883191338`](https://web.archive.org/web/20040820203739/http://www.3anet.co.jp/english/text_e_m_trans.html)|  みんなの日本語初級Ⅰ 第２版 翻訳・文法解説 フランス語版<br>[`ISBN : 9784883196456`](https://www.3anet.co.jp/np/en/books/2312/) |
| **Book 2**<br>*French Version* | みんなの日本語初級Ⅱ 翻訳・文法解説フランス語版<br>[`ISBN : 9784883191383`](https://web.archive.org/web/20040820203739/http://www.3anet.co.jp/english/text_e_m_trans.html) | みんなの日本語初級Ⅱ 第２版 翻訳・文法解説 フランス語版<br>[`ISBN : 9784883197057`](https://www.3anet.co.jp/np/en/books/2412/) |


## 🚦 Conventions

What I call a *convention* is any rule I set while creating the dataset that is not directly derived from the source material.

<p align="center">
  See 
  <a href="https://github.com/vitto4/MinnaNoDS/blob/main/CONVENTIONS.md">
    <code>CONVENTIONS.md</code>
  </a>
</p>

This file also includes general information about the structure of the dataset.

## 🔖 Notes

- When starting out with this project, I used [Paul Denisowski's vocabulary lists](http://www.denisowski.org/Japanese/Japanese.html) to generate a blank template for me to fill in. Serious time-saver right there !
- As strings in `romaji` do not need to be spellchecked, you may use the following config with [`CSpell`](https://cspell.org/).
  ```json
    "cSpell.ignoreRegExpList": [
        "/romaji:\\s*\"[^\"]*\"/gi"
    ]
  ```
- This project should have shipped with the set of scripts I used to lint and validate the dataset. <br>
  It didn't, but who knows, I may get to it when (if) I stop being obsessed with that one space dwarves simulator ¯\\\_(ツ)_/¯
- Adding or removing a word will alter the `id` of all subsequent words in the same lesson. <br>
  Therefore, any time this has to be done, the version number will have to be bumped to the next major release as this could be considered breaking change for anyone using `id` as a [primary key](## "Which it intends to be, when it is in fact more of something I believed to be called a `natural key` and may thus be unstable.").
- « This must have taken quite the amount of time to make » well you don't say ! (笑) <br>
  Though I think I'm happy with how it turned out c:
- ~~I haven't yet managed to get my hands on a French version of the first edition of book 1, so words found exclusively in `Book 1, edition 1` have no French `meaning` for now~~　—　fixed as of [v1.1.0](https://github.com/vitto4/MinnaNoDS/releases/tag/v1.1.0).



## 🚧 Warning

```yaml
#   * The selection of words and their respective translations are the sole property of 3A Corporation.
#     This dataset and subsequent projects that depend on it shall only be used *in conjunction with* – and not *as a substitute for* – the books ; so as to not cause any financial harm to the IP owners.
#   * As per previous remarks, no commercial use of this file shall be admissible.
```
<p align="center"><sup> More <a href="https://github.com/vitto4/MinnaNoDS/blob/ae20b1408e2752642618312728ff817fe2479dd4/minna-no-ds.yaml#L12-L14">here</a>.</sup></p>

The lack of license is deliberate, as I am uncertain about the appropriate licensing options for this project.
Content isn't mine, only the dataset structure and the actual work of filling it in. <br>
If you know a suitable option, feel free to open an issue !

Hopefully that doesn't stop anyone from using the dataset though.
