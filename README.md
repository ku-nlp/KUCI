# Kyoto University Commonsense Inference dataset (KUCI)

KUCI is a Japanese dataset for training/evaluating the linguistic capability to infer basic contingency (hereafter, **commonsense contingency reasoning**).
This dataset comprises 104k multiple-choice questions that ask basic contingency.
It is also characterized by its semi-automatic construction method: automatic extraction of pairs of basic event expressions that have contingent relation from a raw corpus, verification through crowdsourcing, and automatic generation of commonsense contingency reasoning problems from the verified pairs.
Here is an example of the commonsense contingency reasoning problem:

```text
電池の減りはやはり早いので、 (The battery drains so fast that)
  a. 実際の半導体製造装置は実現しません (actual semiconductor manufacturing equipment is not realized)
  b. 今回は期間限定でのお届けになります (it is a limited-time offer this time)
  c. 原子炉を手動停止する ({I} manually shut down a nuclear reactor)
  d. 充電用にＵＳＢケーブル買います ({I} buy a USB cable for charging)
※ {} denotes a dropped pronoun.
```

The task is to choose the most appropriate choice as the continuation of a given context.
In this case, _d_ is a correct choice.

##### Definitions of Terms

cf. [2], [3]

- **contingency**: the discourse relation between events established when one is likely to cause the other
- **core event**: high-frequency predicate-argument structure (acquired from case frames)
- **base**: pair of a context and a correct choice constituting each problem

### Statistics

| Train  | Dev    | Test   |
|--------|--------|--------|
| 83,127 | 10,228 | 10,291 |

In addition, 862k pseudo-problems are available.

- [Download pseudo-problems (98MB)](https://nlp.ist.i.kyoto-u.ac.jp/nl-resource/KUCI/pseudo_problems.tar.gz)

### Data Format

The data format is JSON Lines.

```json lines
{
  "id": 0,
  "context": "電池 の 減り は やはり 早い ので 、",
  "choice_a": "実際 の 半導体 製造 装置 は 実現 し ませ ん",
  "choice_b": "今回 は 期間 限定 で の お 届け に なり ます",
  "choice_c": "原子 炉 を 手動 停止 する",
  "choice_d": "充電 用 に ＵＳＢ ケーブル 買い ます",
  "label": "d",
  "agreement": 2,
  "core_event_pair": "減り/へりv,ガ,早い/はやい|ケーブル/けーぶる,ヲ,買う/かう"
}
```

| Key                 | Type | Description                                                                                |
|---------------------|------|--------------------------------------------------------------------------------------------|
| id                  | int  | unique whole number for each problem (0-origin)                                            |
| context             | str  | context (segmented into morphemes using Juman++ Version: 2.0.0-rc3)                        |
| choice_{a, b, c, d} | str  | choice (〃)                                                                                 |
| label               | str  | letter corresponding to a correct choice (any of {a, b, c, d})                             |
| agreement           | int  | number of crowdworkers who agreed that the base has contingent relation (any of {2, 3, 4}) |
| core_event_pair     | str  | pair of core events constituting the base                                                  |

### License

After internal discussion, we have determined to license this dataset under the [Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/).
If you find any problem, please contact us by e-mail at "nl-resource at nlp.ist.i.kyoto-u.ac.jp" or "omura at nlp.ist.i.kyoto-u.ac.jp".  
(" at " = @)

<a href="https://creativecommons.org/licenses/by-sa/4.0/"><img src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png"/></a>

### External Links

- [Website](https://nlp.ist.i.kyoto-u.ac.jp/EN/?KUCI)
- [Demo (in Japanese)](https://lotus.kuee.kyoto-u.ac.jp/~omura/app/KUCI/)
  - You can try some training examples
- [Pseudo-problems (98MB)](https://nlp.ist.i.kyoto-u.ac.jp/nl-resource/KUCI/pseudo_problems.tar.gz)

### Reference/Citation

[1] (Omura et al., 2020)
```
@inproceedings{omura-etal-2020-method,
  title = "{A} {M}ethod for {B}uilding a {C}ommonsense {I}nference {D}ataset based on {B}asic {E}vents",
  author = "Omura, Kazumasa and
    Kawahara, Daisuke and
    Kurohashi, Sadao",
  booktitle = "Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP)",
  month = nov,
  year = "2020",
  address = "Online",
  publisher = "Association for Computational Linguistics",
  url = "https://aclanthology.org/2020.emnlp-main.192/",
  doi = "10.18653/v1/2020.emnlp-main.192",
  pages = "2450--2460",
}
```

[2] (Omura & Kurohashi, 2022)
```
@inproceedings{omura-kurohashi-2022-improving,
  title = "{I}mproving {C}ommonsense {C}ontingent {R}easoning by {P}seudo-data and its {A}pplication to the {R}elated {T}asks",
  author = "Omura, Kazumasa and
    Kurohashi, Sadao",
  booktitle = "Proceedings of the 29th International Conference on Computational Linguistics",
  month = oct,
  year = "2022",
  address = "Gyeongju, Republic of Korea",
  publisher = "International Committee on Computational Linguistics",
  url = "https://aclanthology.org/2022.coling-1.68/",
  pages = "812--823",
}
```

[3] (Omura et al., 2023)
```
@article{omura-etal-2023-building,
  title = "{B}uilding a {C}ommonsense {I}nference {D}ataset based on {B}asic {E}vents and its {A}pplication",
  author = "Omura, Kazumasa and
    Kawahara, Daisuke and
    Kurohashi, Sadao",
  journal = "Journal of Natural Language Processing",
  volume = "30",
  number = "4",
  year = "2023",
  doi = "10.5715/jnlp.30.1206",
  pages = "1206-1239",
  note = "(in Japanese)",
}
```
