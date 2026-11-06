# AI Translation and AI Text-to-Speech for a Personal Korean Sentence List: Quality, Pitfalls, Costs

Research date: 2026-11-06. Research limits: several hosts were blocked in this session (azure.microsoft.com, learn.microsoft.com, arxiv.org, videostew.com), and the Google Cloud pricing page returned truncated content. Some figures therefore come from search-result excerpts of official pages or from third-party aggregators. This is flagged per item. Anything marked "[unverified, background knowledge]" comes from the researcher's prior knowledge (cutoff mid-2026), not from a source fetched in this session. The report writer should treat those items as leads, not as facts.

## Q1. English->Korean translation quality: Papago vs Google vs DeepL vs LLMs

### Takeaway
No rigorous public benchmark compares all of these tools on casual, first-person English->Korean. WMT25 added English->Korean with expert MQM human evaluation, and frontier LLMs (Gemini 2.5 Pro, GPT-4.1) were the top systems overall in WMT25. Blog and user consensus says Papago is the strongest of the dedicated MT apps for Korean, and DeepL is the weakest of the three for Korean. An LLM is the only option that lets you specify speech level and context, which matters most for this use case.

### Cited Findings
- WMT25 (the main academic MT competition, 2025) included English->Korean as a new pair, and evaluated it with the MQM expert-annotation schema rather than the lighter ESA protocol used for most pairs — [Findings of WMT25 General MT (ACL Anthology)](https://aclanthology.org/anthology-files/pdf/wmt.real/2025.wmt-1.1.pdf); [Findings of WMT25, preview](https://preview.aclanthology.org/setup/2025.wmt-1.22)
- The WMT25 preliminary (automatic-metric) ranking has an English-Korean table that includes Claude-4 among the systems. The authors say the official human-evaluation ranking supersedes it. Per-system Korean scores could not be read in this session because arxiv.org was blocked — [Preliminary Ranking of WMT25 General MT Systems](https://arxiv.org/html/2508.14909v2)
- Secondary coverage of WMT25: Gemini 2.5 Pro and GPT-4.1 led overall, and Gemini 2.5 Pro was in the top cluster for 14 of 16 pairs. These are aggregate results, not English-Korean figures — [Slator: WMT25 preliminary results](https://slator.com/wmt25-preliminary-results-gemini-2-5-pro-gpt-4-1-lead-ai-translation/); [Lara Translate blog](https://blog.laratranslate.com/translation-model-benchmark/)
- WMT24's main general task did not clearly cover Korean. WMT24 did add English<->Korean to its *chat* translation task: 8 teams, 22 primary submissions, and UNBABEL-IT best on most pairs — search summary of [WMT24 findings](https://preview.aclanthology.org/setup/2024.wmt-1.1)
- WMT24++ extends the WMT24 test set to 55 languages and dialects (Korean included). It collected 0-shot outputs from Claude 3.5 Sonnet, GPT-4o and Gemini 1.5 Pro, and had to remove 38 verbose segments, mostly from Claude 3.5 (it added commentary instead of a bare translation) — [WMT24++ paper](https://arxiv.org/pdf/2502.12404)
- Blog and app-review consensus: Papago beats Google Translate on Korean accuracy, and DeepL is "not as accurate as Papago for Korean". Google is preferred for travel features (camera, voice). These are marketing-adjacent blogs, not benchmarks — [Lingopie](https://lingopie.com/blog/best-korean-translator-apps/); [LiveSmartKorea, Dec 2025](https://livesmartkorea.blogspot.com/2025/12/papago-vs-google-translate-korea-2025.html); [machinetranslation.com, Jan 2025](https://www.machinetranslation.com/blog/google-translate-vs-papago); [Linguise](https://linguise.com/blog/guide/navers-papago-vs-google-translate-which-one-better)
- One 2026 comparison site (methodology unclear, SEO-style) reports Papago leading Korean-English (95.1%), ChatGPT and Claude close behind (4.2 and 4.1 out of 5), and Claude rated higher on nuance and tone — [tools-34m comparison 2026](https://tools-34m.pages.dev/en/ai-translation-quality-comparison-chatgpt-claude-gemini-papago-deepl-en/). Another SEO-style page says GPT-4 leads English->Korean on "speech levels and natural phrasing", based on 3 sample sentences — [nllb-com EN->KO](https://nllb-com.pages.dev/english-to-korean-translation). Both are weak evidence.
- An r/Korean thread "deepL or naver papago?" exists (10 upvotes, 15 comments), but its answers could not be read (mirror site) — [r/Korean mirror](https://red.ks32.dev/r/Korean/comments/1jtclin/deepl_or_naver_papago)
- A Korean-language error analysis of *Pachinko* dialogue found fewer total errors (lexical, grammatical, omission, mechanical) from ChatGPT than from Papago — [IJCON journal 21(3):138](https://www.accesson.kr/ijcon/assets/pdf/57464/journal-21-3-138.pdf) (search-summary level)
- SemEval-2025 Task 2 (Team ACK) studied "beyond word-for-word" English-Korean MT, covering entity- and culture-aware translation — [arXiv 2504.20451](https://arxiv.org/html/2504.20451v1) (title and abstract level only)

### Inferences
- For short casual sentences about daily life and skateboarding, the main risk is register and naturalness, not raw accuracy. An LLM given explicit instructions (see Q2) is likely the best fit, because Papago, Google and DeepL take no context or speech-level instructions. (Papago has had an honorific toggle in its app [unverified, background knowledge].)
- A practical workflow: generate with an LLM (Claude, GPT or Gemini), then cross-check against Papago. Where the two differ substantially, flag the sentence for native review.
- LLM translation is effectively free at this scale. 3,000 short sentences is roughly 100–200k tokens in and out, which costs cents on any API or nothing on a free chat tier. No pricing for this was fetched in this session.

### Gaps
- Per-system English->Korean scores from WMT25 (human MQM) could not be extracted: arxiv.org was blocked and the ACL PDF was not fetched. Whether Papago was evaluated in WMT25 is unknown.
- No independent benchmark of casual, spoken-style or slang English->Korean was found.
- The r/Korean consensus content was not retrievable.

## Q2. Typical errors and how to prompt an LLM to avoid them

### Takeaway
Known failure modes include mixing speech levels within one text or exchange (반말/해요체/합니다체), stiff, literal or "translationese" phrasing, and register mismatch. Vendor sources name speech-level mixing as a specific weakness of LLMs, including Claude. The usual fix is to state the speech level, the speaker and listener relationship, and the setting explicitly in the prompt, and to tell the model to drop subjects and pronouns the way natural Korean does.

### Cited Findings
- Automated tools often misapply 존댓말 (polite) vs 반말 (casual) forms, so the tone comes across as stiff or disrespectful — [Linguise: Korean website translation](https://www.linguise.com/blog/guide/korean-website-translation-how-to-avoid-common-problems-and-do-it-right/)
- Speech-level mixing is named as Claude's weakness for English->Korean, and NLLB-200 mixes casual and formal endings within a single utterance — [nllb-com EN->KO](https://nllb-com.pages.dev/english-to-korean-translation) (SEO-style source)
- A Korean-rater job listing describes LLMs "sliding between formal and casual within a single exchange" as a known model failure that raters are hired to catch — [remowork Korean specialist listing](https://remowork.life/jobs/6ad2c25c6821d16bb339f51c/korean-specialist)
- A 2026 ACL paper (Cihlar et al., "Investigating the Automatic Translation of Korean Honorifics") tests translation models on honorifics with and without explicit context. Only the description was seen, not the results — [ACL Anthology author page](https://aclanthology.org/people/luis-cihlar/)
- Machine translation and honorifics: reliability concerns are discussed by a translation vendor — [Somya Translations](https://www.somyatrans.com/?p=37091)

### Inferences
- Pronoun overuse (당신, 그녀, 너), literal idioms, subject over-specification and odd loanword choices are widely discussed by Korean teachers, but no citable source was retrieved in this session. Background knowledge [unverified]: 당신 is rarely used to address someone in conversation and can sound confrontational or romantic-couple-like. 그녀 is mostly literary. Natural Korean omits 나는/저는 when the subject is obvious. Skateboarding slang usually stays as English loanwords (킥플립, 알리, 보드 타다), and an engine may produce a literal Korean rendering or a non-standard spelling.
- Suggested prompt elements (derived from the error types above, not from a tested source):
  - "Translate into natural spoken Korean as a [20s] Korean would say it to [a close friend of the same age] (반말) / [a new acquaintance] (해요체). Use the same speech level in every sentence."
  - "Drop subjects and pronouns where a native speaker would. Never use 당신 or 그녀."
  - "Translate idioms and slang by meaning, not word for word. For skateboarding terms, use the loanwords Korean skaters actually use."
  - "Output only the Korean sentence, then a literal English gloss, then a one-line note on anything uncertain." The gloss and note help a non-speaker review; WMT24++ saw Claude add unrequested commentary, so it is better to ask for explanation in a fixed format.
  - For shadowing, a learner usually benefits from consistent 해요체 (polite, safe default) unless the goal is talking with peers. Choosing one level avoids learning mixed habits.

### Gaps
- No quantitative data on how often each engine makes pronoun, speech-level or idiom errors.
- No sourced, tested prompt templates for Korean register control were found.

## Q3. How a non-speaker can verify sentences

### Takeaway
Back-translation alone is unreliable. A stiff, word-for-word Korean sentence often back-translates perfectly, and register, style and naturalness are invisible to it. Better approaches: cross-check two engines (LLM vs Papago), ask the LLM for a literal gloss plus uncertainty notes, and send a sample, especially flagged sentences, to native speakers (HiNative, HelloTalk, Tandem, r/Korean).

### Cited Findings
- "A bad or literal translation will often produce an excellent back translation". A stilted version tends to come back cleanly while a natural one may look unfaithful — [Dynamic Language: The Back-Translation Dilemma](https://dynamiclanguage.com/the-back-translation-dilemma); [LangPro: back translation pros and cons](https://www.langpro.com.au/back-translation-the-pros-and-cons/)
- Back-translation "will not reflect the quality of the translation with regards to style or register" and won't necessarily flag poor style or grammar. A third-party review is recommended instead — [LangPro](https://www.langpro.com.au/back-translation-the-pros-and-cons/)
- Back-translation looks for conceptual equivalence, not fluency — [RWS glossary](https://www.rws.com/glossary/back-translation)
- Third-party blogs recommend testing the same sentences in several tools and comparing them — [machinetranslation.com](https://www.machinetranslation.com/blog/google-translate-vs-papago)

### Inferences
- Tiered QA for a learner on a few-dollar budget:
  - (1) The LLM produces Korean plus a gloss.
  - (2) Papago or Google translates the Korean back to English, to catch meaning errors only, not naturalness.
  - (3) Run the same English through Papago. Big structural differences become a "review" flag.
  - (4) A second LLM pass as a "native editor" ("Is this natural spoken Korean in 해요체? Rewrite if not and explain") catches some register mixing.
  - (5) Native spot-checks of about 5–10% of sentences plus all flagged ones, on HiNative, HelloTalk or Tandem (free tiers) or r/Korean. Batch about 5–10 sentences per post so helpers are not overloaded.
- TTS can also act as a check: if the TTS stumbles or sounds odd on a sentence, that sometimes points to a spelling or spacing problem.

### Gaps
- No sourced data on HiNative, HelloTalk or Tandem correction quality, response times, or free-tier limits (HiNative's free-tier limits are known to have changed over time [unverified]).
- No r/Korean rules on translation-check requests were retrieved.

## Q4. Korean TTS options, 2026 pricing, naturalness, and Korean-specific issues

### Takeaway
All major cloud TTS services support Korean, and the free tiers easily cover a 1,000–3,000-sentence list. Google Cloud gives 4M free characters a month for Standard/WaveNet and 1M for Neural2 and Chirp 3 HD. Azure Neural gives 0.5M a month. Known Korean TTS weak spots are numbers (native vs Sino-Korean readings by counter), symbols and units, loanwords, and some phonological rules (ㄴ/ㄹ assimilation, tensification). These are mostly avoidable by writing numbers out in Hangul.

### Cited Findings
Pricing (verify on live pages before budgeting):
- **Google Cloud TTS**, from the official pricing-table excerpt plus aggregators that agree with it:
  - Standard and WaveNet: 0–4M characters a month free, then $4 per 1M.
  - Neural2: 1M free, then $16 per 1M.
  - Studio: 1M free, then $160 per 1M.
  - Chirp 3: HD: 1M free a month, then $30 per 1M ($0.00003 per character).
  - Instant custom voice: no free tier, $60 per 1M.
  - Gemini-TTS models are billed by tokens and are not in this free tier.
  - Sources: [Google Cloud TTS pricing (nl locale)](https://cloud.google.com/text-to-speech/pricing?hl=nl); [CostBench](https://costbench.com/software/ai-voice-tools/google-cloud-text-to-speech/); [diyai.io](https://diyai.io/ai-tools/audio-generation/google-cloud-text-to-speech-pricing/). No dated official changelog was found.
- **Google Chirp 3: HD** has 30 voice styles across various languages. Whether ko-KR is in the Chirp 3 HD list could not be confirmed because the table was truncated — [Chirp 3: HD docs](https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd); [voice types (ko)](https://cloud.google.com/text-to-speech/docs/voice-types?hl=ko). Korean was added to the Long Audio Synthesis API in March 2025 — [Cloud TTS release notes](https://docs.cloud.google.com/text-to-speech/docs/release-notes?authuser=0)
- **Azure Neural TTS**:
  - Free tier (F0): 0.5M neural characters a month, at most 3,000 characters per file. The free tier is separate from the paid S0 tier — [Azure China pricing page](https://www.azure.cn/en-us/pricing/details/cognitive-services/); [Microsoft Q&A](https://learn.microsoft.com/en-us/answers/questions/1337460/azure-cognitive-speech-tts-is-the-free-tier-includ)
  - Paid rate: $15 per 1M (developersdigest, citing the Azure retail price API, East US, dated Oct 18 2026) vs $16 per 1M (texttolab). This conflict is unresolved — [developersdigest](https://www.developersdigest.tech/models/speech/azure); [texttolab](https://texttolab.com/blog/azure-text-to-speech-pricing)
  - One third-party article claims 5M free characters, which contradicts the official 0.5M for neural voices.
- **OpenAI gpt-4o-mini-tts**: $0.60 per 1M text input tokens and $12 per 1M audio output tokens, about $0.015 per minute of audio — [OpenAI model page](https://developers.openai.com/api/docs/models/gpt-4o-mini-tts); [s-anand.net cost analysis](https://www.s-anand.net/blog/openai-tts-cost/); [Eden AI](https://www.edenai.co/expert-models/openai-gpt-4o-mini-tts). A dated snapshot "gpt-4o-mini-tts-2025-12-15" exists — [Maxim](https://www.getmaxim.ai/bifrost/llm-cost-calculator/provider/openai/model/gpt-4o-mini-tts-2025-12-15). No source on Korean accent quality was found.
- **ElevenLabs**:
  - Free plan: 10,000 credits a month, no commercial rights.
  - Starter: $5 or $6 a month for 30,000 credits (sources disagree).
  - Standard models cost 1 credit per character, and Flash/Turbo models 0.5 credit per character.
  - API Flash/Turbo: about $0.05 per 1,000 characters.
  - Sources: [Smallest.ai](https://smallest.ai/blog/elevenlabs-pricing-explained-plans-limits-hidden-costs-calculator); [TechJack](https://techjacksolutions.com/ai-tools/elevenlabs/elevenlabs-pricing/); [BigVU 2026](https://bigvu.tv/blog/elevenlabs-pricing-2026-plans-credits-commercial-rights-api-costs/)
  - No Korean-specific billing or quality info was found.
- **Naver CLOVA Voice** (NAVER Cloud Premium TTS API):
  - Pay-as-you-go, with a base fee once the service is created even with no calls. 2,000 characters per call.
  - The policy requires live API calls. Saving or reusing generated audio files requires the separate CLOVA Dubbing service, which makes CLOVA Voice a poor fit for building a saved audio deck.
  - Actual rates appear only in the NCP console.
  - Sources: [CLOVA Voice overview](https://guide.ncloud-docs.com/docs/en/clovavoice-overview); [CLOVA Voice policy](https://guide.ncloud-docs.com/docs/en/clovavoice-policy); [API docs](https://api.ncloud-docs.com/docs/ai-naver-clovavoice)
- **Edge TTS (free)**: unofficial clients (Python `edge-tts` by rany2, and ports) reverse-engineer the Edge browser "Read Aloud" WebSocket at speech.platform.bing.com and can use any Microsoft neural voice by short name. Microsoft rotates a protocol constant, so clients can break, and no official terms cover this use — [kothok-edge-tts docs](https://docs.rs/crate/kothok-edge-tts/latest)

Korean-specific TTS pronunciation issues:
- A Chung-Ang University study tested a commercial TTS ("GT") on /ㄴ/+/ㄹ/ sequences. 53 of 232 words had non-standard pronunciation, most involving the Sino-Korean suffix 론 — [scholarworks CAU /ㄴㄹ/ study](https://scholarworks.bwise.kr/cau/handle/2019.sw.cau/38456?mode=full). Related papers cover loanword pronunciation problems in Korean TTS (hangeulization, word-initial tensification) — [CAU loanword TTS paper](https://scholarworks.bwise.kr/cau/handle/2019.sw.cau/52034?mode=full) — and tensification (경음화) errors — [CAU 경음화 paper](https://scholarworks.bwise.kr/cau/handle/2019.sw.cau/38408?mode=full). Only metadata or abstracts were seen.
- English-centric multilingual TTS handles Korean numbers, symbols and units poorly. "Relying solely on English-centric text processing can lead to synthesis instability and pronunciation errors" — [2026 conference abstract](https://d2j16w31g89z0j.cloudfront.net/site/2026w/abs/0759-BZDTX.pdf)
- Counters switch numbers to native Korean (하나/한, 둘/두 ...) while measurement units use Sino-Korean (일, 이 ...). A developer blog describes preprocessing that maps 1–99 to the correct words so that every TTS engine reads them properly — [Videostew blog](https://videostew.com/en/blog/26966-ux-details-to-make-all-tts-engines-properly-read-korean) (search summary; page blocked)
- Older Korean TTS made many errors on Arabic numerals and symbols — [Interspeech 2004, Nam et al.](https://www.isca-archive.org/interspeech_2004/nam04_interspeech.html)

### Inferences
- Have the LLM write all numbers, times and counters out in Hangul (e.g., "세 시 반", "두 번") so the audio is unambiguous. This also teaches the learner the correct reading.
- Naturalness ranking (background knowledge, [unverified]): Google Chirp 3 HD, Azure neural and newer multilingual voices, and ElevenLabs multilingual models are generally considered the most natural. Google Standard is the most robotic. OpenAI TTS voices are tuned toward English and may carry a slight non-native prosody in Korean. Treat this as a hypothesis to test by listening.
- Azure ko-KR voice names [unverified, learn.microsoft.com blocked]: ko-KR-SunHiNeural (F), ko-KR-InJoonNeural (M), ko-KR-HyunsuMultilingualNeural (M), and others such as BongJin, GookMin, JiMin, SeoHyeon, SoonBok and YuJin.
- For a personal study deck, Google's free 4M Standard/WaveNet and 1M Chirp 3 HD, or Azure's 0.5M free, are the cleanest options with clear terms. Edge TTS is free but unofficial and fragile.
- Android's built-in Google TTS engine can read Korean offline for free (installable voice data) [unverified, background knowledge]. Saving audio from it usually needs a third-party app.

### Gaps
- ko-KR availability in Chirp 3 HD and the exact ko-KR voice lists for Google and Azure were not confirmed.
- No head-to-head naturalness test (MOS) for Korean across vendors was found.
- No Korean-specific quality reports for OpenAI TTS or ElevenLabs.
- No CLOVA Voice per-character price.
- Exact Azure paid rate: $15 vs $16 per 1M, unresolved.

## Q5. Rough cost for 1,000–3,000 short sentences

### Takeaway
At about 15–25 Korean characters per short sentence, 3,000 sentences is about 45k–75k characters. That is within every major free tier except ElevenLabs Free. The realistic cost is $0 (Google/Azure free tiers) to about $2–6 (OpenAI or one month of ElevenLabs Starter). Translation by LLM adds cents.

### Cited Findings
- Google: Standard/WaveNet 4M chars/month free, Chirp 3 HD and Neural2 1M/month free — [Google Cloud TTS pricing](https://cloud.google.com/text-to-speech/pricing?hl=nl)
- Azure: 0.5M neural chars/month free — [Azure China pricing](https://www.azure.cn/en-us/pricing/details/cognitive-services/)
- OpenAI gpt-4o-mini-tts: about $0.015 per audio minute — [s-anand.net](https://www.s-anand.net/blog/openai-tts-cost/)
- ElevenLabs: Free 10k credits a month, Starter $5–6 for 30k credits, 1 credit per character on standard models and 0.5 on Flash/Turbo — [Smallest.ai](https://smallest.ai/blog/elevenlabs-pricing-explained-plans-limits-hidden-costs-calculator)

### Inferences
These worked numbers are the researcher's own arithmetic; the sentence-length assumptions are not sourced.
- 3,000 sentences x about 20 characters = 60k characters.
  - Google: $0 on any tier, well inside the free tier. Even beyond the free tier, Chirp 3 HD at $30/1M would cost $1.80.
  - Azure: $0, since 60k is under 500k.
  - ElevenLabs: 60k credits on standard models means 2 months of Starter (about $10–12), or 1 month on Flash/Turbo at 0.5 credit per character (about $5–6). The free tier alone would take 6 months.
  - OpenAI: about 3,000 x 2.5 s = 125 min, so about $1.90.
  - Generating two voices (male and female) doubles character use but still fits the Google and Azure free tiers.
- Google Cloud and Azure free tiers usually require a billing account or credit card at signup [unverified]. Remind the user to set a budget alert.

### Gaps
- Actual average character counts for this user's sentences are unknown.
- Whether Google counts Hangul syllables as 1 character each was not checked in docs. Assumed yes.

## Q6. Speech-to-text for capturing English narration

### Takeaway
Android's built-in voice typing (Gboard / Google voice typing) is free and adequate for dictating English. OpenAI's transcription API is cheap if recordings are batch-processed: Whisper and gpt-4o-transcribe cost about $0.006 a minute, and gpt-4o-mini-transcribe about $0.003 a minute.

### Cited Findings
- whisper-1 and gpt-4o-transcribe cost about $0.006 a minute ($0.36 an hour), and gpt-4o-mini-transcribe about $0.003 a minute ($0.18 an hour). A newer "GPT Transcribe" at $0.0045 a minute was reported by one aggregator and is unverified — [CostGoat](https://costgoat.com/pricing/openai-transcription); [CostBench Whisper](https://costbench.com/software/ai-transcription-apis/openai-whisper/); [besthub.dev](https://besthub.dev/articles/openai-unveils-new-stt-and-tts-models-gpt-4o-transcribe-gpt-4o-mini-transcribe-and-gpt-4o-mini-tts-performance-pricing-and-demo-e42b467daaf5)
- Billing is per minute, so speeding audio up 2–3x before sending it cuts cost — [Gigazine](https://gigazine.net/gsc_news/en/20250627-openai-transcription-api)

### Inferences
- 60 minutes of narration a month costs about $0.18–0.36 via the API. Android voice typing is $0. Open-source Whisper can also run locally for free on a PC (background knowledge [unverified]).
- Speaking in short, complete sentences while narrating makes downstream translation cleaner.

### Gaps
- No sourced accuracy comparison of Android voice typing vs Whisper for casual English with skate jargon.

## Q7. Korean speech recognition for checking the learner's own pronunciation

### Takeaway
Using Korean ASR (Google voice typing set to Korean, or Azure) as a pronunciation check is a reasonable, cheap proxy: if it transcribes what you meant, you are probably intelligible. Research shows ASR accuracy drops for non-native speech, and the evidence for learning gains from ASR feedback is small and mixed. Whether Azure Pronunciation Assessment supports ko-KR could not be confirmed in this session.

### Cited Findings
- ASR has been faulted for low recognition accuracy for L2 learners (study of 117 Korean university students using ASR feedback) — [koreascience 2017](https://koreascience.kr/article/JAKO201732060955528.pdf)
- Learners taught to use ASR for pronunciation practice showed "small but significant improvements" in pronunciation accuracy (Dillon and Wells 2023, *English Education*). Note that this concerns Korean learners of English, not English speakers learning Korean — [koreascience 2023](https://koreascience.kr/article/JAKO202322149979896.pdf)
- A Whisper-based pronunciation assessment study found ASR struggles with accented speech but can give immediate feedback — [ETRI/koreascience](https://www.koreascience.or.kr/article/JAKO202322149979896.page?&lang=ko)
- Research on Korean-as-L2 ASR: training only on L1 Korean speech can be adapted to improve recognition of Korean L2 speech, which means off-the-shelf ASR is weaker on learner Korean — [arXiv 2306.02534](https://arxiv.org/pdf/2306.02534v1.pdf)
- Azure Speech lists ko-KR for speech-to-text. Language support varies by feature, and the pronunciation-assessment table was not visible in search results — [Azure language support](https://learn.microsoft.com/azure/ai-services/speech-service/language-support?tabs=stt); [Azure language learning overview](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/language-learning-overview). A 2023 Azure blog said pronunciation assessment covered more than 10 languages — [Azure blog](https://azure.microsoft.com/en-us/blog/3-microsoft-azure-ai-product-features-that-accelerate-language-learning/)
- Google Cloud Speech-to-Text Chirp 3 supports ko-KR (speech recognition, not TTS) — [Chirp 3 STT model](https://cloud.google.com/speech-to-text/v2/docs/chirp_3-model?hl=en)

### Inferences
- Background knowledge [unverified]: Azure Pronunciation Assessment added ko-KR (accuracy, fluency and completeness scores) by 2023–2024. Azure's free F0 tier includes some free speech-to-text hours a month, and pronunciation assessment is billed as STT. Confirm on the language support page, which was blocked here.
- Google and Android ASR uses a strong language model, so it may "auto-correct" mispronunciations into the expected word. A correct transcript is not proof of correct pronunciation, especially for familiar phrases. Comparing a recording of yourself side by side with the TTS audio is a useful complement.

### Gaps
- No sourced numbers on Google or Android ko-KR ASR accuracy for English-native learners.
- Azure Pronunciation Assessment ko-KR support and pricing were not confirmed (learn.microsoft.com and azure.microsoft.com blocked in this session).
