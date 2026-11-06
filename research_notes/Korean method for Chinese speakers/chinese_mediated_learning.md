# Learning Korean through Chinese, English, or both: a Taiwan-raised Traditional Chinese and English bilingual

Research notes, compiled 2026-11-06. Constraint note: in this session WebFetch could not reach several hosts (docs.ankiweb.net and creatrip.com did not resolve), so most findings below come from search-result abstracts and snippets, not full texts. Items marked [UNVERIFIED] are the researcher's background knowledge with no source retrieved in this session. The report writer should treat them as hypotheses, not cited facts.

## 1. SLA evidence: L1 vs L2 as the mediating language, L3 models, and which language is dominant

### Takeaway
Meta-analytic evidence leans toward L1 glosses for vocabulary learning, but the advantage is modest and shows up mostly on immediate tests. One meta-analysis found no clear effect of gloss language. So "use the language you actually think in" is a sensible default, not a strong law. L3 theory (TPM, CEM) gives no direct Korean-specific verdict, but it supports using both known languages. Arriving abroad at 14 is past the usual dominance-switch window (about 9 to 12), so Chinese may still be dominant, but that depends on the person's later language use and should be self-assessed.

### Cited Findings
- Yanagisawa, Webb and Uchihara (2020), meta-regression in *Studies in Second Language Acquisition*: 359 effect sizes, 42 studies, N = 3,802. L1 glosses produced more vocabulary learning than L2 glosses. Multiple-choice glosses worked best; in-text glosses and glossaries worked least well. — [Cambridge SSLA](https://cambridge.org/core/journals/studies-in-second-language-acquisition/article/how-do-different-forms-of-glossing-contribute-to-l2-vocabulary-learning-from-reading/38124150D59DF3039EE1FF5AE88FE922)
- Kim, Lee and Lee (2024), meta-analysis in *Language Teaching Research*: 78 effect sizes, 26 studies. The L1-gloss advantage appeared mainly on immediate vocabulary posttests, not on delayed posttests or reading comprehension. — [todoele.net bibliography entry](https://www.todoele.net/bibliografia/relative-effects-l1-and-l2-glosses-l2-learning-meta-analysis)
- Zhang and Ma (2024), meta-analysis of textual glosses in *Language Teaching Research*: gloss language had no definite effect on vocabulary acquisition. Gloss location and mode did matter. — [todoele.net bibliography entry](https://todoele.net/bibliografia/effect-textual-glosses-l2-vocabulary-acquisition-meta-analysis). This partly contradicts the two meta-analyses above.
- Tadayonifar et al. (2021), *Journal of Language and Education*: L1 glosses beat L2 glosses for vocabulary, with no difference for reading comprehension. — [HSE JLE PDF](https://jle.hse.ru/article/download/11020/12935)
- Caveat: almost all gloss studies test receptive learning while reading. None found tests productive active recall (L1 prompt to L2 production) for speaking, which is the learner's actual use case. — inferred from the abstracts above
- Typological Primacy Model (Rothman): transfer into an L3 comes from whichever earlier language is judged structurally closest. Similarity is assessed in order: lexicon, then phonology, then functional morphology, then syntax. — [Rothman et al., *Bilingualism: Language and Cognition*](https://www.cambridge.org/core/journals/bilingualism-language-and-cognition/article/linguistic-and-cognitive-motivations-for-the-typological-primacy-model-tpm-of-third-language-l3-transfer-timing-of-acquisition-and-proficiency-considered/56606CE09ED7FEA6DA3F2437C6D31B94)
- Cumulative Enhancement Model (Flynn et al.): all previously learned languages can help later language acquisition, and transfer is facilitative or neutral. — [Overview of L3 models, Benjamins *Linguistic Approaches to Bilingualism*](https://www.benjamins.com/catalog/lab.20055.sch)
- A Taiwanese (NTNU) thesis on L3 Japanese found learners relied more on the typologically closer language (Korean) than the psychotypologically closer one (Chinese). — [NTNU thesis record](https://etds.lib.ntnu.edu.tw/thesis/detail/0364b895370c4c74849a0d4082818d81)
- A Flinders University thesis on Korean–Mandarin bilinguals learning English as an L3 reports they seemed to benefit from prior Korean knowledge. — [Flinders thesis](https://theses.flinders.edu.au/view/34ab8c48-012d-4ed5-89fd-f35cf415f67e/1)
- No study was found that tests TPM against CEM for Chinese–English bilinguals learning Korean as an L3. — search results above
- Dominance and age of arrival: in a study of Chinese-speaking immigrant children, arrival at ages 9 to 12 was the cutoff. Younger arrivals ended up with higher L2 than L1 proficiency, and older arrivals showed the reverse. A three-year follow-up found children arriving at 9 or younger switched preference to L2 within a year, while older arrivals kept L1 dominant. — reported in search snippet summarizing [Cambridge core-reader article](https://www.cambridge.org/core/product/8E0EED4564882B4DCFAC764C5A035C7C/core-reader) (full text not retrieved)
- Israeli data on Soviet immigrant children: most of the drop happened at arrival ages 9 to 14. — [NBER conference paper](https://conference.nber.org/conf_papers/f217035/f217035.pdf)
- Heritage-language children in Canada (2026 longitudinal study): older arrival age went with stronger Arabic, but all children plateaued or lost Arabic and shifted to English dominance over time. — [PMC article](https://pmc.ncbi.nlm.nih.gov/articles/PMC3478675) (search snippet; the PMC ID and 2026 date did not obviously match, so flag for checking)

### Inferences
- Someone who left Taiwan at 14 arrived after the 9-to-12 switch window. They probably have a solid, literate Chinese base (around 9 years of Taiwanese schooling, including Traditional characters). Whether English has since become dominant depends on how many years they have lived in English and what they use daily. Dominance is domain-specific: skate slang, tech, and adult life topics may be English-dominant, while family and emotional topics may be Chinese-dominant.
- Practical rule for active recall prompts: make the prompt in whichever language the learner would naturally narrate that sentence in. That is the language the meaning is stored in, and the gloss meta-analyses favor the stronger or native language. Because this varies by domain, the app should allow per-card prompt-language choice, not one global setting.
- By TPM, Chinese is the likely source of lexical transfer, through Sino-Korean cognates. Lexicon is the first similarity cue, and roughly half or more of Korean vocabulary is Sino-Korean (see section 3). English offers only loanwords (konglish), which matter a lot in skate vocabulary (킥플립 kickflip, 보드 board, 파크 park). Neither language is close to Korean in syntax (Korean is SOV with agglutinative morphology).
- CEM supports "both": show the Chinese prompt plus a Hanja hint for Sino-Korean words, and keep English available for loanwords and slang.

### Gaps
- No study of productive (L1-to-L2) recall that compares L1 and L2 prompt languages.
- No TPM or CEM study with Chinese–English bilinguals learning Korean.
- No validated quick self-test for dominance was retrieved. The Bilingual Language Profile (BLP) is a known tool [UNVERIFIED in this session].

## 2. Machine translation: Korean to zh-TW vs Korean to English, regional wording, and prompt design

### Takeaway
No rigorous independent benchmark of Korean to Traditional Chinese MT was found. Papago supports Traditional Chinese and is widely, though anecdotally, considered strong for Korean. LLMs are measurably weaker in Traditional Chinese and Taiwan usage than in Simplified Chinese, so the risk of Mainland vocabulary and simplified-character leakage is real and should be controlled in the prompt and by checks.

### Cited Findings
- Papago lists Chinese (Simplified) and Chinese (Traditional) as separate languages. It supports around 14 to 15 languages, compared with Google's 100+. — [Wikipedia: Naver Papago](https://Www.Wikipedia.org/wiki/Naver_Papago); [App Store TW listing](https://apps.apple.com/tw/app/id1147874819); [Linguise comparison](https://linguise.com/blog/guide/navers-papago-vs-google-translate-which-one-better)
- Naver claimed its tests showed Korean, English, Japanese and Chinese output about 27% more accurate than other services on average. This is a vendor claim with no methodology given. — [Korea Times 2019](https://www.koreatimes.co.kr/business/tech-science/20190423/navers-papago-app-outperforming-googles-translation-service)
- Blog comparisons say Papago is often better for Korean and for short, conversational sentences, but give no test data. — [machinetranslation.com](https://www.machinetranslation.com/blog/google-translate-vs-papago); [livesmartkorea blog 2025](https://livesmartkorea.blogspot.com/2025/12/papago-vs-google-translate-korea-2025.html)
- TMMLU+ benchmark: models score better when the test is converted to Simplified Chinese, and Traditional-Chinese-tuned models trail Simplified ones. Example of terminology divergence: "computer memory" is 内存 in the Mainland and 記憶體 in Taiwan, so naive character conversion gives wrong terms. — [arXiv 2403.01858](https://arxiv.org/html/2403.01858v3)
- TMLU (Taiwanese Mandarin) benchmark: models are mostly built in a Simplified Chinese context, and Taiwan-tailored open models still lag. It also found Simplified Chinese contamination inside TMMLU+. — [arXiv 2403.20180](https://arxiv.org/html/2403.20180v1)
- SC-TC-Bench tests regional term choice: asking a model to name an item that is called differently in the Mainland and in Taiwan. — [arXiv 2505.22645](https://ar5iv.labs.arxiv.org/html/2505.22645)

### Inferences
- Pipeline: generate Korean with an LLM (better at context, register, and slang), then cross-check with Papago (Korean to zh-TW and to English). If the two disagree, flag the card.
- Recommended LLM prompt elements for Chinese-mediated cards:
  1. "Write Chinese in Taiwan-standard Traditional Chinese (臺灣華語, 正體字). Use Taiwanese vocabulary: 捷運 not 地鐵, 影片 not 視頻, 網路 not 網絡, 軟體 not 軟件, 計程車 not 出租車, 腳踏車 not 自行車, 便利商店 not 便利店, 品質 not 質量 (for quality), 訊息 not 信息. Never output Simplified characters."
  2. "Korean in 해요체 (polite informal, ending -아요/-어요) by default. Also give a 반말 version when the context is peers at a skatepark." Skaters of similar age will likely switch to 반말 quickly. Whether to drop 존댓말 should be the Korean speaker's call (반말 해도 돼요? "Can I speak casually?").
  3. "For every Sino-Korean word, give the Hanja in Traditional form plus the Taiwanese reading, e.g. 학교 (學校), 연습 (練習). Mark false friends where Korean meaning differs from Taiwanese usage." Example: Korean 공부 (工夫) means "study", while Chinese 工夫 means "time or effort". [Example UNVERIFIED as a sourced claim; well known]
  4. "Mark konglish and English loanwords, e.g. 킥플립 (kickflip)."
  5. Output strict JSON with fixed keys for ingestion.
- Post-processing check: run the zh output through OpenCC s2tw or s2twp and diff it, or check for Simplified-only code points. If OpenCC changes anything, Simplified characters leaked. A small blocklist of Mainland terms (地鐵, 視頻, 軟件, 質量…) catches vocabulary leakage that character conversion cannot. [OpenCC behavior UNVERIFIED in this session]
- Korean to English translation is likely more reliable for LLMs overall, given more training data [inference]. A reasonable default is to generate Korean from whichever language the user narrated in, then back-translate to the other language as a check.

### Gaps
- No academic BLEU, COMET, or human-evaluation study comparing Papago, Google, DeepL, and LLMs on Korean to zh-TW. Late-2026 rankings are unknown.
- DeepL's support for Korean and for Traditional Chinese was not verified in this session. [UNVERIFIED: DeepL added Korean in 2023 and Traditional Chinese around 2024 to 2025.]

## 3. Korean-learning resources in Traditional Chinese for Taiwanese learners

### Takeaway
There are solid Taiwan-published textbooks (日月文化's 《首爾大學韓國語》 and the newer 《首爾大學韓國語+》). Chinese speakers get a real vocabulary head start because about 57% of the Standard Korean Language Dictionary is Sino-Korean. Searches failed to verify specific Taiwanese YouTube teachers, a zh-TW Duolingo Korean course, or Chinese-speaker Anki decks. These need manual checking.

### Cited Findings
- 《首爾大學韓國語》 is published in Taiwan by 日月文化, written by 首爾大學語言教育院. It has six levels, each split into A and B volumes, sold with MP3 audio. — [誠品 3B listing](https://www.eslite.com/product/1001276402502161)
- New edition 《首爾大學韓國語+》 (3A shown, with a grammar booklet and QR-code online audio, also as an e-book). — [誠品 3A e-book](https://www.eslite.com/product/10072302132683193173003)
- 《首爾大學韓國語+》 1A, 1B, 2A and 2B (textbook and workbook with QR-code audio), dated 2024 to 2025, appear in NCCU's catalog. — [NCCU repository](https://nccur.lib.nccu.edu.tw/ir/handle/140.119/153790)
- Sino-Korean share of vocabulary: estimates range from 30% to 70%. The National Institute of Korean Language's Standard Korean Language Dictionary is about 57% Sino-Korean. — [Wikipedia: Sino-Korean vocabulary](https://en.wikipedia.org/wiki/Sino-Korean_vocabulary)
- Limits of the advantage: native Korean words, grammar, honorifics and pronunciation get no help from Chinese. — [Myna blog "Anti-Bridge List"](https://myna-220.pages.dev/blog/korean-for-chinese-speakers); [discoverdiscomfort blog](https://discoverdiscomfort.com/?p=5764). These are blogs.
- An academic study (Ca' Foscari) found learners see hanja education as important but often irrelevant to beginner and everyday conversation. It warns that poorly presented hanja semantic networks can entrench misconceptions. — [iris.unive.it](https://iris.unive.it/handle/10278/5101435)
- Talk To Me In Korean (TTMIK) is recommended on Chinese-language sites but teaches in English. — [Creatrip (search snippet)](https://creatrip.com/news/9102)
- KBS World offered a basic Korean course with a Chinese interface (2014 article, possibly outdated). — [Business Weekly 數位時代/Smart](https://smart.businessweekly.com.tw/Reading/WebArticle.aspx?id=53760)
- Duolingo: Korean is its 7th most popular language, and it launched Traditional Chinese interface apps in 2013 (for learning English). No zh-TW-to-Korean course was confirmed. — [zum news](https://news.zum.com/articles/97688994/k-content-fuels-global-korean-learning-boom-surpassing-chinese-on-duolingo); [SCMP](https://amp.scmp.com/lifestyle/technology/article/1570019/language-learning-app-duolingo-makes-waves-chinese-market)

### Inferences
- With only a few dollars and one month, a ~NT$500 to 600 textbook is optional. The best free Chinese-mediated tools are Papago (zh-TW) and Naver's 中韓辭典 (zh.dict.naver.com) [UNVERIFIED that it displays Traditional characters; it is believed to be Simplified-primary]. Use the English-medium TTMIK and Naver English–Korean dictionary for slang and loanwords.
- Hanja helps from day one only if it is used as a reading aid on cards (學校 to 학교). The learner should not "study hanja" as a separate subject this month, consistent with the Ca' Foscari finding.
- [UNVERIFIED, needs manual check] Duolingo has historically offered Korean courses for Chinese speakers (via a Chinese UI), and LingoDeer has offered Chinese-interface Korean. Status in late 2026 is unknown.

### Gaps
- Could not verify any named Taiwanese YouTube or podcast creator teaching Korean in Chinese. Searches returned only Korean vloggers and lifestyle channels. Manual search terms to try: 「韓文自學」「韓語40音」「韓文發音」 on YouTube, and PTT Korea board or Dcard 韓語板 recent threads.
- Could not verify 博客來 listings or prices. Only 誠品 listings were found. 延世韓國語 Taiwan editions were not checked.
- AnkiWeb shared decks for Chinese speakers or Hanja decks were not checked (ankiweb.net not reachable here).
- Naver Chinese dictionary Traditional-character support and Taiwan-usage coverage were unconfirmed.

## 4. Chinese-speaking communities, language exchange, and usefulness of Chinese in Seoul

### Takeaway
Chinese–Korean language exchange exists in Seoul (Hongdae and Sinchon meetups, HelloTalk). There is also a sizable Taiwanese working-holiday cohort (about 800 H-1 visas per year, per a blog). No evidence was found of a Taiwanese or Chinese-speaking skater community in Seoul.

### Cited Findings
- A Hongdae international language exchange runs English–Korean sessions Wednesday to Saturday, with a Chinese–Korean section on Wednesdays. — [Airbnb experience listing](https://www.airbnb.com.au/experiences/3634744)
- A Sinchon meetup offers Korean, Japanese, Chinese, English, Spanish and German exchange. — [Meetup Sinchon](https://www.meetup.com/sinchon-language-culture-exchange-meet-up-신촌역)
- "Seoul Language Exchange" Meetup group covers English, Korean, Japanese and Chinese. — [Meetup](https://www.meetup.com/seoul-language-exchange-make-korean-international-friends/)
- HelloTalk lists Korean speakers wanting to learn Chinese (Chinese ⇄ Korean exchange pages). — [HelloTalk](https://www.hellotalk.com/it/partners/exchange/chinese-to-korean)
- Somoim is a Korean app for in-person club activities. — [gogohanguk guide](https://gogohanguk.com/en/blog/find-korean-language-exchange-in-seoul)
- Taiwan–Korea working holiday (H-1): 800 places per year, age limit 35, up to 1,300 hours of work per year. Blog source, not official. — [uptogo.com.tw](https://uptogo.com.tw/國際/韓國打工/)

### Inferences
- Since Korean learners of Chinese mostly study Mandarin, a Taiwanese learner can offer Mandarin plus Traditional characters as a trade. Mention 「臺灣華語」 up front, since many Korean learners study Simplified.
- Chinese is probably useful in tourist zones (Myeongdong, duty-free shops, some restaurant staff) [UNVERIFIED]. At skateparks, English plus Korean is more likely to be useful than Chinese [inference].
- To meet skaters, Instagram hashtags such as #서울스케이트보드 and local skate shops are likely better than language-exchange groups [UNVERIFIED].

### Gaps
- No source on Taiwanese or Chinese-speaking skaters in Seoul.
- No data on how widely Mandarin is spoken in Seoul service jobs.

## 5. App and data design implications

### Takeaway
Store one note per sentence with all language fields, and generate prompt cards per chosen prompt language (zh-TW, English, or both). Korean TTS is the only audio needed. Android handles Hangul and CJK fonts and Korean input natively. Anki's note-type and card-template system can likely do all of this, but official docs could not be fetched for confirmation.

### Cited Findings
- Hanja-reading value depends on Sino-Korean share, about 57% of dictionary headwords. — [Wikipedia: Sino-Korean vocabulary](https://en.wikipedia.org/wiki/Sino-Korean_vocabulary)
- Benchmarks show Traditional Chinese and Taiwan-term weaknesses in LLMs. The app should validate the zh field. — [arXiv 2403.01858](https://arxiv.org/html/2403.01858v3)

### Inferences
- Suggested card fields:
  - `ko`: Korean sentence in 해요체
  - `ko_banmal`: optional casual version
  - `ko_romanization`: optional, hide by default
  - `hanja_gloss`: e.g. 연습(練習) 하다
  - `zh_tw`: Taiwan Traditional Chinese
  - `en`: English
  - `source_lang`: which language the learner narrated in
  - `prompt_langs`: zh, en, or both
  - `audio_ko` (normal speed), `audio_ko_slow`
  - `notes`: grammar, false friends, konglish
  - `register`: 해요체, 반말, 합쇼체
  - `niche_tags`: e.g. skate, daily, food
  - `verified_by`: e.g. Papago or a native speaker
- Make the prompt language a per-user default with a per-card override, and offer a "dual prompt" mode (zh plus en) for ambiguous sentences. This generalizes to any learner and niche: fields such as `native` and `bridge` instead of hardcoded zh and en.
- Audio: Korean TTS only. Chinese or English TTS is unnecessary because the learner reads those. The free option is Android's built-in Google TTS with Korean voice data, or Edge/Azure neural Korean voices [UNVERIFIED pricing and terms].
- Fonts [UNVERIFIED]: Android ships Noto Sans CJK (Source Han), which covers Hangul and Traditional Han characters. In web or PWA builds, set `lang="ko"` on Korean text and `lang="zh-Hant-TW"` on Chinese text so the correct regional glyphs are chosen. Without this, Hanja may render in Japanese or Simplified glyph shapes.
- Input [UNVERIFIED]: Gboard supports adding a Korean (2-beolsik) layout alongside 注音 (Zhuyin) or English and switching with the globe key. The laptop needs a Korean IME (e.g. Windows Microsoft IME Korean, or ibus-hangul or fcitx5-hangul on Linux). Typing Korean answers during recall forces spelling practice, but speaking aloud is closer to the skatepark goal.
- AnkiDroid [UNVERIFIED, docs.ankiweb.net blocked]: one note type can have several card templates, e.g. "zh→ko", "en→ko", "ko→meaning (listening)". Conditional generation with `{{#Field}}...{{/Field}}` lets a card exist only when a field such as `prompt_zh` is non-empty, so the user picks prompt languages per note. `{{type:ko}}` gives type-in-answer, and `{{tts ko_KR:ko}}` gives on-device TTS as a fallback to recorded audio.
- Cost: LLM generation of a few hundred sentences plus Papago web or app checks fits within a few dollars [inference; check current API pricing].

### Gaps
- Official Anki manual pages on templates and conditional replacement could not be fetched. Confirm the syntax before building.
- Android TTS Korean voice quality vs neural cloud voices: no comparative source retrieved.
- Late-2026 Papago API availability and pricing for third-party apps not checked (Naver Cloud Papago API terms) [UNVERIFIED].
