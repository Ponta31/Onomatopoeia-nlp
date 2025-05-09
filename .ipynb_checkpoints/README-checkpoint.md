# Japanese Onomatopoeia Paraphraser Model

_This project applies Word2Vec model to paraphrase a word in a Japanese sentence to a similar onomatopoeia. The purpose of this model is to help students in Japanese class learn Japanese onomatopoeia, since the Japanese language is very rich with onomatopoeia._

---

## Key Feature
- POS tagging
- Word2Vec model trained on a corpus and onomatopoeia sentences
- semantic similarity matching between regular words and onomatopoeia


---

## Repository Structure

```
onomatopoeia-nlp
├── datasets
│   ├── onomatope_list.txt
│   └── onomatope_sentences.txt
├── environment.yml   #virtual environment for the model
├── Onomatope_article.pdf
├── paraphraser_model.ipynb   #Main script
├── README.ipynb　  #This was converted to md file
└── README.md #This is the project instruction
```


---

## Datasets
- `onomatope_list.txt`：List of onomatopoeia (335 onomatopoeia)
- `onomatope_sentences.txt`：Sentences containing onomatopoeia for training (https://www2.ninjal.ac.jp/Onomatope/50_on.html)
- `OSCAR-2301`：Japanese language corpus（Hugging Face）
  * size:258.7 GB
  * docs:36,328,931
  * words:5,592,948,356

---

## Setup Instruction

1. Clone the repository
   ```
   git clone https://github.com/Ponta31/Onomatopoeia-nlp.git
   
   ```


#### | _**NOTE**: Please make sure to modify file paths in the code to match your system._


2. Create and activate the virtual environment

   ```
   conda env create -f environment.yml
   conda activate onomato-env
   
   ```


3. Run the notebook



---
## Paraphrasing Rules

The model follows specific syntactic patterns to identify which words to replace:

1. If the sentence contains adverb + adjective + verb in sequence, it paraphrases the adjective
2. If the sentence contains adverb + verb in sequence, it paraphrases the verb
3. If the sentence contains an adjective without a verb, it paraphrases the adjective
4. If only a verb is contained without adjectives or adverbs, it inserts an onomatopoeia in front of the verb

---

## Result Analysis
The model generated the following outputs. When the target word was either an adverb or an adjective, the model replaced it with an onomatopoeia. For verbs, the model inserted an onomatopoeia immediately before the verb.
As a native Japanese speaker, I evaluated each suggested onomatopoeia for semantic appropriateness. In patterns 1 and 2 (involving adverbs and adjectives), I marked with an "S" those onomatopoeia that were somewhat semantically similar to the target word's meaning within a context. For pattern 3 (involving verbs), I marked with an "S" those cases where the onomatopoeia appropriately matched the verb. Cases that were semantically inappropriate were marked with an "X".

The accuracy rates for each pattern were:

- **Result1(Adverbs)**:8/30(26%)
- **Result2(Adjectives)**: 7/30(23%)
- **Result3(Verbs)**: 5/35(14%)

These results indicate that while the model shows some ability to match onomatopoeia with appropriate words, there is significant room for improvement in semantic alignment. The relatively low accuracy rates highlight the challenges in computational modeling of Japanese onomatopoeia, which often have subtle contextual and emotional connotations that are difficult to capture with the current approach.


#### Pattern 1: Adverb to onomatopoeia
Similar onomatopoeia of 遅く(slowly, lately)  Top 5：
- ジメジメ: 0.6864 | x
- ぐったり: 0.6815 | x
- ぐっすり: 0.6734 | x
- ぎりぎり: 0.6651 | S
- メチャメチャ: 0.6647 | x

Similar onomatopoeia of おそく(slowly, lately)  Top 5：
- メチャメチャ: 0.8546 | x
- ガックリ: 0.8528 | x
- カンカン: 0.8342 | x
- ぐしゃぐしゃ: 0.8319 | x
- ごつごつ: 0.8303 | x

Similar onomatopoeia of 早く(quickly)  Top 5：
- イライラ: 0.6549 | x
- ぐっすり: 0.6529 | x
- がっかり: 0.6280 | x
- ジメジメ: 0.6212 | x
- モリモリ: 0.6148 | x

Similar onomatopoeia of はやく(quickly)  Top 5：
- コッテリ: 0.8709 | x
- ザラザラ: 0.8703  | x
- ギクシャク: 0.8602 | x
- アッサリ: 0.8563 | S
- ウロウロ: 0.8549 | x

Similar onomatopoeia of 激しく(aggresively, intensely)  Top 5：
- ぐんぐん: 0.7755 | x
- グイグイ: 0.7667 | S
- ジメジメ: 0.7504 | x
- ぐっと: 0.7358 | S
- イライラ: 0.7255 | x

Similar onomatopoeia of はげしく(aggresively, intensely)  Top 5：
'はげしく' is not in the vocabulary.
no words in word2vec

Similar onomatopoeia of 強く(strongly)  Top 5：
- ぐんぐん: 0.7068 | S
- モリモリ: 0.6954 | S
- ぐっと: 0.6867 | x
- くっきり: 0.6619 | S
- グイグイ: 0.6534 | S

Similar onomatopoeia of つよく(strongly)  Top 5：
'つよく' is not in the vocabulary.
no words in word2vec

_**Result1**:8/30(26%)_

---

#### Pattern 2: Adjective to onomatopoeia
Similar onomatopoeia of きれい(beautiful)  Top 5：
- モリモリ: 0.6682 | x
- クルクル: 0.6584 | x
- くっきり: 0.6508 | S
- キョロキョロ: 0.6408 | x
- さっと: 0.6403 | x

Similar onomatopoeia of やわらかい(soft)  Top 5：
- しっとり: 0.8759 | x
- こんがり: 0.8232 | x
- ゴシゴシ: 0.8223 | x
- ほんのり: 0.8070 | x
- シャキシャキ: 0.8053 | x

Similar onomatopoeia of 静か(quiet)  Top 5：
- モリモリ: 0.6682 | x
- ぐったり: 0.6607 | x
- わいわい: 0.6499 | x
- ぐいぐい: 0.6348 | x
- おっとり: 0.6257 | S

Similar onomatopoeia of しずか(quiet)  Top 5：
'しずか' is not in the vocabulary.
no words in word2vec

Similar onomatopoeia of 楽しい(fun)  Top 5：
- ワクワク: 0.7128 | S
- ワイワイ: 0.6901 | S
- めちゃめちゃ: 0.6825 | x
- ぐっと: 0.6513 | x
- ころころ: 0.6489 | x

Similar onomatopoeia of たのしい(fun)  Top 5：
- うだうだ: 0.7752 | x
- わいわい: 0.7744 | S
- シッカリ: 0.7653 | x
- ポンポン: 0.7573 | x
- もりもり: 0.7539 | x

Similar onomatopoeia of にぎやか(lively)  Top 5：
- げっそり: 0.8616 | x
- ぐんぐん: 0.8461 | x
- わいわい: 0.8436 | S
- メチャメチャ: 0.8412 | x
- ワイワイ: 0.8392 | S

_**Result2**: 7/30(23%)_

---

#### Pattern 3: Add an onomatopoeia in front of the verb(dictionary form) 

Similar onomatopoeia of 歩く(to walk)  Top 5：
- じっと: 0.6458 | x
- こつこつ: 0.6444 | S
- きらきら: 0.6287 | x
- うろうろ: 0.6197 | S
- げっそり: 0.6164 | x

Similar onomatopoeia of あるく(to walk)  Top 5：
- ザラザラ: 0.9031 | x
- ガサガサ: 0.8997 | x
- うんと: 0.8996 | x
- ゴツゴツ: 0.8946 | x
- ゴタゴタ: 0.8943 | x

Similar onomatopoeia of 降る(to rain)  Top 5：
- ジメジメ: 0.7663 | x
- うんざり: 0.7361 | x
- ぐったり: 0.7345 | x
- じめじめ: 0.7303 | x
- ころころ: 0.7191 | x

Similar onomatopoeia of 揺れる(to quake)  Top 5：
- ごろごろ: 0.8578 | x
- ころころ: 0.8460 | x
- くるくる: 0.8312 | x
- くっきり: 0.8299 | x
- ほんのり: 0.8298 | x

Similar onomatopoeia of ゆれる(to quake)  Top 5：
- げんなり: 0.8542 | x
- グッタリ: 0.8527 | x
- コッテリ: 0.8462 | x
- がさがさ: 0.8450 | S
- ぎくしゃく: 0.8398 | x

Similar onomatopoeia of 笑う(to laugh)  Top 5：
- げらげら: 0.8411 | S
- ガンガン: 0.8390 | x
- ワイワイ: 0.8382 | x
- がっかり: 0.8365 | x
- めちゃめちゃ: 0.8344 | S

Similar onomatopoeia of 言う(to say)  Top 5：
- ぼんやり: 0.6887 | x
- じめじめ: 0.6785 | x
- めちゃくちゃ: 0.6706 | x
- モリモリ: 0.6680 | x
- メチャクチャ: 0.6660 | x


_**Result3**: 5/35(14%)_

---

#### Pattern 3.5: Add an onomatopoeia in front of the verb(present progressive form) 

Similar onomatopoeia of 歩いています(is walking)  Top 5：
'歩いています' is not in the vocabulary.
no words in word2vec

Similar onomatopoeia of あるいています(is walking)  Top 5：
'あるいています' is not in the vocabulary.
no words in word2vec

Similar onomatopoeia of 揺れている(is quaking)  Top 5：
'揺れている' is not in the vocabulary.
no words in word2vec

Similar onomatopoeia of ゆれている(is quaking)  Top 5：
'ゆれている' is not in the vocabulary.
no words in word2vec



---

## Limitations and Future Work

- **Limited onomatopoeia sentences**: The current dataset contains fewer than 100 onomatopoeia sentences, which is not sufficient for training.

- **Word2Vec limitaions**: Due to the limited dataset of onomatopoeia sentences, the model may not capture proper meanings of onomatopoeia expressions. Also, Word2Vec can only consider words within a defined window, and doesn't account for broader context.

- **Recognition of conjugated words**: The model doesn't recognize different conjugation forms, such as '歩く'(dictionary form) and '歩いている'(present progressive form).

- **Recognition of different styles of Japanese**: Japanese writing has three styles (Hiragana, Katakana, Kanji), and the model recognizes those separately.

___Future improvements___:
- Use Web scraping technique to collect more examples of onomatopoeia sentences.

- Implement RNN or LSTM to improve contextual understanding.

- Modify the model to recognize conjugated words and Japanese different writing styles through lemmatization or morphological analysis.

---


## Conclusion

Due to the challenges in capturing the nuanced meanings of Japanese onomatopoeia, the current model did not perform as well as intended. However, with the future improvements above, this tool could become a valuable resource for students striving to master Japanese expressions. By employing both NLP and language pedagogy, this project has demonstrated the potential of an innovative approach to Japanese language learning. 


---

## References
- Huang, H. (2021). Onomatopoeia in the Japanese educational vocabulary: A corpus-based survey. Tokyo University of Foreign Studies, Journal of the Institute of Language Research, 26, 25-46.