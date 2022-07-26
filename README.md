# nnsvs-chinese-support
Hed and supporting files for Chinese NNSVS Dataset Creation

This repo includes the files required to create a fully functional Chinese dataset for use in NNSVS, with additional instructions and examples provided (or to be provided) for the labeling process.

The phoneme set is a custom made one in consideration to character limitations of NNSVS based on a mix of pinyin and X-Sampa for standard Mandarin, with additional phonemes for support of the Hokkien/Taiwanese dialect.

Note that since there is currently no pretrained model available for use, it is expected that for a high quality result, around 6 hours or more of audio (excluding silence) to be needed. However, 2 to 3 hours of audio data (excluding silence) should be sufficent for a decent quality model, with less (~1 hours worth) audio data (excluding silence) sufficient for a prototype test.

Here is a render of a model with 3 hours of data, tuned in OpenUtau

https://user-images.githubusercontent.com/107520869/180795817-5e91bee3-0a6b-44fe-aef5-4179ee74b9e8.mp4

## Additional Info
The hed file provided in this repository was hand-written specifically for NNSVS and may not work with other platforms/programs as-is. Two hed files are provided, a full length one in addition to a minimal one, while both are fully functional, it's recommended to use the full length one.

"Phoneme Explanations.txt" includes all phonemes available for the Chinese language support with reference to their usage, the bold text within the words refer to the phoneme pronunciation in said words.

Within the /dic folder is a dictionary made for NNSVS to allow for pinyin input for simpler input, with additonal support for Japanese due to the extended phoneme support made for the Hokkien/Taiwanese dialect. The pinyin section of the dictionary is heavily modified based on the default dictionary supplied for Synthesizer V while the Japanese section is modified from the default Japanese dictionary provided within the ENUNU training kit.

The hed file used for training can be changed via the config.yaml, found at `/train/config.yaml` within the ENUNU training kit.

Note that the "in_dim" value found in `/conf/train/*/model/*.yaml` used for training must be changed accordingly to the hed file, the values should be set up as follows if using "chinese.hed":
* acoustic_conv.yaml: 372
* acoustic_rmdn.yaml: 372
* duration_lstm.yaml: 368
* duration_mdn.yaml: 368
* timelag_ffn.yaml: 368
* timelag_mdn.yaml: 368

If using "chinese_MDN.hed", use the following settings: (note that this certain hed file is useful when training the rMDN, MDN, and RMDN model types.)
* acoustic_conv.yaml: 272
* acoustic_rmdn.yaml: 272
* duration_lstm.yaml: 268
* duration_mdn.yaml: 268
* timelag_ffn.yaml: 268
* timelag_mdn.yaml: 268

Training will not work without setting up these values correctly

As of the current version, the hed includes tone flags available for altering the tone due to ENUNU's flag system, with a simple flag of `i` that ranges from i1 to i8, how the flags are assigned to different tones are completely up to you.

# nnsvs-korean-sub-language-support
The secondary dictionary named `korean.table` in /dic is for allowing Chinese databases to sing in Korean.
NOTE: This is not an official language support and may have quality issues, this is merely made for broadening the usage of existing Chinese databases.

The dictionary is based off of romanized Hangul for easier input when using [ENUNU](https://github.com/oatsu-gh/ENUNU).
NOTE: This is made with the Chinese language in mind and so it may differ a bit from standard romanized Hangul, please refer to the dictionary or view below for correct usage. Also, some vowels were removed due to pronunciation limitations, such as ㅐ, ㅒ, ㅙ, and ㅚ.

ㅔ instead of `e` is `ee/E` (ee is the dictionary entry, E is the phoneme, both work), ㅠ is `yuu/YU`. The above are exceptions to prevent existing phonemes to override eachother and cause issues, the rest should follow regular romanized Hangul.

Here is demo of this dictionary being used on our beta vocal ACV-M1, the song used is Way Back Home by Shuan. 

https://user-images.githubusercontent.com/107520869/180787114-db1d0569-67a5-4b2e-923d-b41cc9131362.mp4
