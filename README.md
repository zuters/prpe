# PRPE segmentator

This repository contains text segmentation scripts for machine translation.

## The main principles

  - Performs close-to-morphological segmentation
  - For the present, tuned for English and Latvian languages
  - Requires minor adaptation for using in other languages:
  -- small source code changes
  -- tuning of hyperparameters
  - to support open-vocabulary, segmented texts should be post-processed using [BPE]

   [BPE]: <https://github.com/rsennrich/subword-nmt>
