# PRPE (Prefix-Root-Postfix-Encoding) segmentator

This repository contains text segmentation scripts for machine translation: [learn_prpe.py], [apply_prpe.py], [unprocess_prpe.py], [prpe.py].

## The main principles

  - Performs close-to-morphological segmentation
  - For the present, tuned for English and Latvian languages
  - Requires minor adaptation for using in other languages:
  -- small source code changes
  -- tuning of hyperparameters
  - to support open-vocabulary, segmented texts should be post-processed using [BPE]
  - python 2/3 compatible

## Usage instructions

PRPE is used in the following way:
  - Learning phase (files of potential segments produced): learn_prpe.py
  - Segmentation phase (using produced files of the previous phase): apply_prpe.py
  - Removing segmentation: unprocess_prpe.py

### Phase #1. Learning

During this phase several 'code' files are produced from the {corpus} representing building blocks for the segmentation:
  - {prefixes}
  - {roots}
  - {suffixes}
  - {postfixes} (actually in the lastest version this particular file is redundant for segmentation)
  - {endings}
  - vocabulary of most frequent {words} to avoid segmentation

Running the learning script:

```sh
(python) ./learn_prpe.py -i {corpus} -p {prefixes} -r {roots} -s {suffixes} -t {postfixes} -u {endings} -w {words} -a {prefix rate} -b {suffix rate} -c {postfix rate} -v {vocabulary size} -l {langugae}
```

where:
  -- prefix rate: how many prefixes to collect (greater than 1 means exact number, less means percentage)
  -- suffix rate: how many suffixes to collect (greater than 1 means exact number, less means percentage)
  -- postfix rate: how many postfixes to collect (greater than 1 means exact number, less means percentage) (in the latest version this particular parameter is redundant)
  -- vocabulary size: how many the most frequent words to store to avoid segmentations for them (in order to reduce number of segments)
  -- language: for the present, only 'lv' and 'en' are acceptable; otherwise 'en' scripts to check word parts will be switched

All the rates (prefix, suffix, postfix, vocabulary) should be experimentally tuned. Conditions for roots and endings (not represented in parameters) are hardcoded.

Example configuration used for Latvian (produced files see in 'codefiles-lv' directory):
```sh
(python) ./learn_prpe.py -i input.lv -p prefixes.lv -r roots.lv -s suffixes.lv -t postfixes.lv -u endings.lv -w words.lv -a 32 -b 1000 -c 0.1 -v 5000 -l lv
```

Example configuration used for English (produced files see in 'codefiles-en' directory):
```sh
(python) ./learn_prpe.py -i input.en -p prefixes.en -r roots.en -s suffixes.en -t postfixes.en -u endings.en -w words.en -a 32 -b 200 -c 180 -v 5000 -l en
```


   [BPE]: <https://github.com/rsennrich/subword-nmt>
   [learn_prpe.py]: <https://github.com/zuters/prpe/learn_prpe.py>
   [apply_prpe.py]: <https://github.com/zuters/prpe/apply_prpe.py>
   [unprocess_prpe.py]: <https://github.com/zuters/prpe/unprocess_prpe.py>
   [prpe.py]: <https://github.com/zuters/prpe/prpe.py>
