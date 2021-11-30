---
title: Language support - Speech service
titleSuffix: Azure Cognitive Services
description: The Speech service supports numerous languages for speech-to-text and text-to-speech conversion, along with speech translation. This article provides a comprehensive list of language support by service feature.
services: cognitive-services
author: eric-urban
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 01/07/2021
ms.author: eur
ms.custom: references_regions, ignite-fall-2021
---

# Language and voice support for the Speech service

Language support varies by Speech service functionality. The following tables summarize language support for [Speech-to-text](#speech-to-text), [Text-to-speech](#text-to-speech), [Speech translation](#speech-translation) and [Speaker Recognition](#speaker-recognition) service offerings.

## Speech-to-text

Both the Microsoft Speech SDK and the REST API support the following languages (locales). 

To improve accuracy, customization is available for some languages and baseline model versions by uploading **Audio + Human-labeled Transcripts**, **Plain Text**, **Structured Text**, and **Pronunciation**. By default, Plain Text customization is supported for all available baseline models. To learn more about customization, see [Get started with Custom Speech](./custom-speech-overview.md).

<!--
To get the AM and ML bits:
https://westus.dev.cognitive.microsoft.com/docs/services/speech-to-text-api-v3-0/operations/GetSupportedLocalesForModels

To get pronunciation bits:
https://cris.ai -> Click on Adaptation Data -> scroll down to section "Pronunciation Datasets" -> Click on Import -> Locale: the list of locales there correspond to the supported locales
-->

| Language                 | Locale (BCP-47) | Customizations  | [Language identification](how-to-automatic-language-detection.md) | [Pronunciation assessment](how-to-pronunciation-assessment.md) |
|------------------------------------|--------|---------------------------------------------------|-------------------------------|--------------------------|
| Arabic (Algeria)                   | `ar-DZ` | Plain Text                                   |                           |                          |
| Arabic (Bahrain), modern standard  | `ar-BH` | Plain Text                                   |                           |                          |
| Arabic (Egypt)                     | `ar-EG` | Plain Text                                   | Yes                          |                          |
| Arabic (Iraq)                      | `ar-IQ` | Plain Text                                   |                           |                          |
| Arabic (Israel)                    | `ar-IL` | Plain Text                                   |                           |                          |
| Arabic (Jordan)                    | `ar-JO` | Plain Text                                   |                           |                          |
| Arabic (Kuwait)                    | `ar-KW` | Plain Text                                   |                           |                          |
| Arabic (Lebanon)                   | `ar-LB` | Plain Text                                   |                           |                          |
| Arabic (Libya)                     | `ar-LY` | Plain Text                                   |                           |                          |
| Arabic (Morocco)                   | `ar-MA` | Plain Text                                   |                           |                          |
| Arabic (Oman)                      | `ar-OM` | Plain Text                                   |                           |                          |
| Arabic (Qatar)                     | `ar-QA` | Plain Text                                   |                           |                          |
| Arabic (Saudi Arabia)              | `ar-SA` | Plain Text                                   |                           |                          |
| Arabic (Palestinian Authority)     | `ar-PS` | Plain Text                                   |                           |                          |
| Arabic (Syria)                     | `ar-SY` | Plain Text                                   |                           |                          |
| Arabic (Tunisia)                   | `ar-TN` | Plain Text                                   |                           |                          |
| Arabic (United Arab Emirates)      | `ar-AE` | Plain Text                                   |                           |                          |
| Arabic (Yemen)                     | `ar-YE` | Plain Text                                   |                           |                          |
| Bulgarian (Bulgaria)               | `bg-BG` | Plain Text                                   |                           |                          |
| Catalan (Spain)                    | `ca-ES` | Plain Text<br>Pronunciation                  | Yes                          |                          |
| Chinese (Cantonese, Traditional)   | `zh-HK` | Plain Text                 |        Yes                   |                          |
| Chinese (Mandarin, Simplified)     | `zh-CN` | Plain Text                 |     Yes                      | Yes                         |
| Chinese (Taiwanese Mandarin)       | `zh-TW` | Plain Text                 |           Yes                |                          |
| Croatian (Croatia)                 | `hr-HR` | Plain Text<br>Pronunciation                  |                           |                          |
| Czech (Czech)             | `cs-CZ` | Plain Text<br>Pronunciation                  |                           |                          |
| Danish (Denmark)                   | `da-DK` | Plain Text<br>Pronunciation                  | Yes                          |                          |
| Dutch (Netherlands)                | `nl-NL` | Plain Text<br>Pronunciation|    Yes                       |                          |
| English (Australia)                | `en-AU` | Plain Text<br>Pronunciation| Yes                          |                          |
| English (Canada)                   | `en-CA` | Plain Text<br>Pronunciation| Yes                          |                          |
| English (Ghana)                    | `en-GH` | Plain Text<br>Pronunciation                  |                           |                          |
| English (Hong Kong)                | `en-HK` | Plain Text<br>Pronunciation                  |                           |                          |
| English (India)                    | `en-IN` | Plain Text<br>Structured Text (20210907)<br>Pronunciation |                          |                          |
| English (Ireland)                  | `en-IE` | Plain Text<br>Pronunciation                  |                           |                          |
| English (Kenya)                    | `en-KE` | Plain Text<br>Pronunciation                  |                           |                          |
| English (New Zealand)              | `en-NZ` | Plain Text<br>Pronunciation |                          |                          |
| English (Nigeria)                  | `en-NG` | Plain Text<br>Pronunciation                  |                           |                          |
| English (Philippines)              | `en-PH` | Plain Text<br>Pronunciation                  |                           |                          |
| English (Singapore)                | `en-SG` | Plain Text<br>Pronunciation                  |                           |                          |
| English (South Africa)             | `en-ZA` | Plain Text<br>Pronunciation                  |                           |                          |
| English (Tanzania)                 | `en-TZ` | Plain Text<br>Pronunciation                  |                           |                          |
| English (United Kingdom)           | `en-GB` | Audio (20201019)<br>Plain Text<br>Structured Text (20210906)<br>Pronunciation| Yes                          | Yes                         |
| English (United States)            | `en-US` | Audio (20201019, 20210223)<br>Plain Text<br>Structured Text (20211012)<br>Pronunciation| Yes                          | Yes                         |
| Estonian(Estonia)                  | `et-EE` | Plain Text<br>Pronunciation                  |                           |                          |
| Filipino (Philippines)             | `fil-PH`| Plain Text<br>Pronunciation                  |                           |                          |
| Finnish (Finland)                  | `fi-FI` | Plain Text<br>Pronunciation                  |     Yes                      |                          |
| French (Canada)                    | `fr-CA` | Audio (20201015)<br>Plain Text<br>Structured Text (20210908)<br>Pronunciation|     Yes                      |                          |
| French (France)                    | `fr-FR` | Audio (20201015)<br>Plain Text<br>Structured Text (20210908)<br>Pronunciation|      Yes                     |                          |
| French (Switzerland)               | `fr-CH` | Plain Text<br>Pronunciation                  |                           |                          |
| German (Austria)                   | `de-AT` | Plain Text<br>Pronunciation                  |                           |                          |
| German (Switzerland)               | `de-CH` | Plain Text<br>Pronunciation                  |                           |                          |
| German (Germany)                   | `de-DE` | Audio (20201127)<br>Plain Text<br>Structured Text (20210831)<br>Pronunciation|  Yes                         |                          |
| Greek (Greece)                     | `el-GR` | Plain Text                                   |  Yes                         |                          |
| Gujarati (Indian)                  | `gu-IN` | Plain Text                                   |                           |                          |
| Hebrew (Israel)                    | `he-IL` | Plain Text                                   |                           |                          |
| Hindi (India)                      | `hi-IN` | Plain Text                 |     Yes                      |                          |
| Hungarian (Hungary)                | `hu-HU` | Plain Text<br>Pronunciation                  |                           |                          |
| Indonesian (Indonesia)             | `id-ID` | Plain Text<br>Pronunciation                  |                           |                          |
| Irish (Ireland)                    | `ga-IE` | Plain Text<br>Pronunciation                  |                           |                          |
| Italian (Italy)                    | `it-IT` | Audio (20201016)<br>Plain Text<br>Pronunciation|      Yes                     |                          |
| Japanese (Japan)                   | `ja-JP` | Plain Text                                   |      Yes                     |                          |
| Kannada  (India)                   | `kn-IN` | Plain Text                                   |                           |                          |
| Korean (Korea)                     | `ko-KR` | Audio (20201015)<br>Plain Text                 |      Yes                     |                          |
| Latvian (Latvia)                   | `lv-LV` | Plain Text<br>Pronunciation                  |                           |                          |
| Lithuanian (Lithuania)             | `lt-LT` | Plain Text<br>Pronunciation                  |                           |                          |
| Malay (Malaysia)                   | `ms-MY` | Plain Text                                   |                           |                          |
| Maltese (Malta)                    | `mt-MT` | Plain Text                                   |                           |                          |
| Marathi (India)                    | `mr-IN` | Plain Text                                   |                           |                          |
| Norwegian (Bokmål, Norway)         | `nb-NO` | Plain Text                                   |     Yes                      |                          |
| Persian (Iran)                     | `fa-IR` | Plain Text                                   |                           |                          |
| Polish (Poland)                    | `pl-PL` | Plain Text<br>Pronunciation                  |       Yes                    |                          |
| Portuguese (Brazil)                | `pt-BR` | Audio (20201015)<br>Plain Text<br>Pronunciation|          Yes                 |                          |
| Portuguese (Portugal)              | `pt-PT` | Plain Text<br>Pronunciation                  |             Yes              |                          |
| Romanian (Romania)                 | `ro-RO` | Plain Text<br>Pronunciation                  |  Yes                         |                          |
| Russian (Russia)                   | `ru-RU` | Plain Text                 |                Yes           |                          |
| Slovak (Slovakia)                  | `sk-SK` | Plain Text<br>Pronunciation                  |                           |                          |
| Slovenian (Slovenia)               | `sl-SI` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Argentina)                | `es-AR` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Bolivia)                  | `es-BO` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Chile)                    | `es-CL` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Colombia)                 | `es-CO` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Costa Rica)               | `es-CR` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Cuba)                     | `es-CU` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Dominican Republic)       | `es-DO` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Ecuador)                  | `es-EC` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (El Salvador)              | `es-SV` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Equatorial Guinea)        | `es-GQ` | Plain Text                                   |                           |                          |
| Spanish (Guatemala)                | `es-GT` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Honduras)                 | `es-HN` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Mexico)                   | `es-MX` | Plain Text<br>Structured Text (20210908)<br>Pronunciation|    Yes                       |                          |
| Spanish (Nicaragua)                | `es-NI` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Panama)                   | `es-PA` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Paraguay)                 | `es-PY` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Peru)                     | `es-PE` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Puerto Rico)              | `es-PR` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Spain)                    | `es-ES` | Audio (20201015)<br>Plain Text<br>Structured Text (20210908)<br>Pronunciation|  Yes                         |                          |
| Spanish (Uruguay)                  | `es-UY` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (USA)                      | `es-US` | Plain Text<br>Pronunciation                  |                           |                          |
| Spanish (Venezuela)                | `es-VE` | Plain Text<br>Pronunciation                  |                           |                          |
| Swahili (Kenya)                    | `sw-KE` | Plain Text                                   |                           |                          |
| Swedish (Sweden)                   | `sv-SE` | Plain Text<br>Pronunciation                  |   Yes                        |                          |
| Tamil (India)                      | `ta-IN` | Plain Text                                   |                           |                          |
| Telugu (India)                     | `te-IN` | Plain Text                                   |                           |                          |
| Thai (Thailand)                    | `th-TH` | Plain Text                                   |      Yes                     |                          |
| Turkish (Turkey)                   | `tr-TR` | Plain Text                                   |                           |                          |
| Vietnamese (Vietnam)               | `vi-VN` | Plain Text                                   |                           |                          |

## Text-to-speech

Both the Microsoft Speech SDK and REST APIs support these voices, each of which supports a specific language and dialect, identified by locale. You can also get a full list of languages and voices supported for each specific region/endpoint through the [voices list API](rest-text-to-speech.md#get-a-list-of-voices). 

> [!IMPORTANT]
> Pricing varies for standard, custom and neural voices. Please visit the [Pricing](https://azure.microsoft.com/pricing/details/cognitive-services/speech-services/) page for additional information.

### Neural voices

Neural text-to-speech is a new type of speech synthesis powered by deep neural networks. When using a neural voice, synthesized speech is nearly indistinguishable from the human recordings.

Neural voices can be used to make interactions with chatbots and voice assistants more natural and engaging, convert digital texts such as e-books into audiobooks and enhance in-car navigation systems. With the human-like natural prosody and clear articulation of words, neural voices significantly reduce listening fatigue when users interact with AI systems.

> [!NOTE]
> Neural voices are created from samples that use a 24 khz sample rate.
> All voices can upsample or downsample to other sample rates when synthesizing.

| Language | Locale | Gender | Voice name | Style support |
|---|---|---|---|---|
| Afrikaans (South Africa) | `af-ZA` | Female | `af-ZA-AdriNeural` <sup>New</sup>  | General |
| Afrikaans (South Africa) | `af-ZA` | Male | `af-ZA-WillemNeural` <sup>New</sup>  | General |
| Amharic (Ethiopia) | `am-ET` | Female | `am-ET-MekdesNeural` <sup>New</sup>  | General |
| Amharic (Ethiopia) | `am-ET` | Male | `am-ET-AmehaNeural` <sup>New</sup>  | General |
| Arabic (Algeria) | `ar-DZ` | Female | `ar-DZ-AminaNeural` <sup>New</sup>  | General |
| Arabic (Algeria) | `ar-DZ` | Male | `ar-DZ-IsmaelNeural` <sup>New</sup>  | General |
| Arabic (Bahrain) | `ar-BH` | Female | `ar-BH-LailaNeural` <sup>New</sup>  | General |
| Arabic (Bahrain) | `ar-BH` | Male | `ar-BH-AliNeural` <sup>New</sup>  | General |
| Arabic (Egypt) | `ar-EG` | Female | `ar-EG-SalmaNeural` | General |
| Arabic (Egypt) | `ar-EG` | Male | `ar-EG-ShakirNeural` | General |
| Arabic (Iraq) | `ar-IQ` | Female | `ar-IQ-RanaNeural` <sup>New</sup>  | General |
| Arabic (Iraq) | `ar-IQ` | Male | `ar-IQ-BasselNeural` <sup>New</sup>  | General |
| Arabic (Jordan) | `ar-JO` | Female | `ar-JO-Sana Neural` <sup>New</sup>  | General |
| Arabic (Jordan) | `ar-JO` | Male | `ar-JO-Taim Neural` <sup>New</sup>  | General |
| Arabic (Kuwait) | `ar-KW` | Female | `ar-KW-NouraNeural` <sup>New</sup>  | General |
| Arabic (Kuwait) | `ar-KW` | Male | `ar-KW-FahedNeural` <sup>New</sup>  | General |
| Arabic (Libya) | `ar-LY` | Female | `ar-LY-ImanNeural` <sup>New</sup>  | General |
| Arabic (Libya) | `ar-LY` | Male | `ar-LY-OmarNeural` <sup>New</sup>  | General |
| Arabic (Morocco) | `ar-MA` | Female | `ar-MA-MounaNeural` <sup>New</sup>  | General |
| Arabic (Morocco) | `ar-MA` | Male | `ar-MA-JamalNeural` <sup>New</sup>  | General |
| Arabic (Qatar) | `ar-QA` | Female | `ar-QA-AmalNeural` <sup>New</sup>  | General |
| Arabic (Qatar) | `ar-QA` | Male | `ar-QA-MoazNeural` <sup>New</sup>  | General |
| Arabic (Saudi Arabia) | `ar-SA` | Female | `ar-SA-ZariyahNeural` | General |
| Arabic (Saudi Arabia) | `ar-SA` | Male | `ar-SA-HamedNeural` | General |
| Arabic (Syria) | `ar-SY` | Female | `ar-SY-AmanyNeural` <sup>New</sup>  | General |
| Arabic (Syria) | `ar-SY` | Male | `ar-SY-LaithNeural` <sup>New</sup>  | General |
| Arabic (Tunisia) | `ar-TN` | Female | `ar-TN-ReemNeural` <sup>New</sup>  | General |
| Arabic (Tunisia) | `ar-TN` | Male | `ar-TN-HediNeural` <sup>New</sup>  | General |
| Arabic (United Arab Emirates) | `ar-AE` | Female | `ar-AE-FatimaNeural` <sup>New</sup>  | General |
| Arabic (United Arab Emirates) | `ar-AE` | Male | `ar-AE-HamdanNeural` <sup>New</sup>  | General |
| Arabic (Yemen) | `ar-YE` | Female | `ar-YE-MaryamNeural` <sup>New</sup>  | General |
| Arabic (Yemen) | `ar-YE` | Male | `ar-YE-SalehNeural` <sup>New</sup>  | General |
| Bangla (Bangladesh) | `bn-BD` | Female | `bn-BD-NabanitaNeural` <sup>New</sup>  | General |
| Bangla (Bangladesh) | `bn-BD` | Male | `bn-BD-PradeepNeural` <sup>New</sup>  | General |
| Bulgarian (Bulgaria) | `bg-BG` | Female | `bg-BG-KalinaNeural` | General |
| Bulgarian (Bulgaria) | `bg-BG` | Male | `bg-BG-BorislavNeural` | General |
| Burmese (Myanmar) | `my-MM` | Female | `my-MM-NilarNeural` <sup>New</sup>  | General |
| Burmese (Myanmar) | `my-MM` | Male | `my-MM-ThihaNeural` <sup>New</sup>  | General |
| Catalan (Spain) | `ca-ES` | Female | `ca-ES-AlbaNeural` | General |
| Catalan (Spain) | `ca-ES` | Female | `ca-ES-JoanaNeural` | General |
| Catalan (Spain) | `ca-ES` | Male | `ca-ES-EnricNeural` | General |
| Chinese (Cantonese, Traditional) | `zh-HK` | Female | `zh-HK-HiuGaaiNeural` | General |
| Chinese (Cantonese, Traditional) | `zh-HK` | Female | `zh-HK-HiuMaanNeural` | General |
| Chinese (Cantonese, Traditional) | `zh-HK` | Male | `zh-HK-WanLungNeural` | General |
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaohanNeural` | General, multiple styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaomoNeural` | General, multiple role-play and styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaoruiNeural` | Senior voice, multiple styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaoxiaoNeural` | General, multiple voice styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaoxuanNeural` | General, multiple role-play and styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaoyouNeural` | Child voice, optimized for story narrating |
| Chinese (Mandarin, Simplified) | `zh-CN` | Male   | `zh-CN-YunxiNeural` | General, multiple styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| Chinese (Mandarin, Simplified) | `zh-CN` | Male | `zh-CN-YunyangNeural` | Optimized for news reading,<br /> multiple voice styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| Chinese (Mandarin, Simplified) | `zh-CN` | Male | `zh-CN-YunyeNeural` | Optimized for story narrating |
| Chinese (Taiwanese Mandarin) | `zh-TW` | Female | `zh-TW-HsiaoChenNeural` | General |
| Chinese (Taiwanese Mandarin) | `zh-TW` | Female | `zh-TW-HsiaoYuNeural` | General |
| Chinese (Taiwanese Mandarin) | `zh-TW` | Male | `zh-TW-YunJheNeural` | General |
| Croatian (Croatia) | `hr-HR` | Female | `hr-HR-GabrijelaNeural` | General |
| Croatian (Croatia) | `hr-HR` | Male | `hr-HR-SreckoNeural` | General |
| Czech (Czech) | `cs-CZ` | Female | `cs-CZ-VlastaNeural` | General |
| Czech (Czech) | `cs-CZ` | Male | `cs-CZ-AntoninNeural` | General |
| Danish (Denmark) | `da-DK` | Female | `da-DK-ChristelNeural` | General |
| Danish (Denmark) | `da-DK` | Male | `da-DK-JeppeNeural` | General |
| Dutch (Belgium) | `nl-BE` | Female | `nl-BE-DenaNeural` | General | 
| Dutch (Belgium) | `nl-BE` | Male | `nl-BE-ArnaudNeural` | General | 
| Dutch (Netherlands) | `nl-NL` | Female | `nl-NL-ColetteNeural` | General |
| Dutch (Netherlands) | `nl-NL` | Female | `nl-NL-FennaNeural` | General |
| Dutch (Netherlands) | `nl-NL` | Male | `nl-NL-MaartenNeural` | General |
| English (Australia) | `en-AU` | Female | `en-AU-NatashaNeural` | General |
| English (Australia) | `en-AU` | Male | `en-AU-WilliamNeural` | General |
| English (Canada) | `en-CA` | Female | `en-CA-ClaraNeural` | General |
| English (Canada) | `en-CA` | Male | `en-CA-LiamNeural` | General |
| English (Hongkong) | `en-HK` | Female | `en-HK-YanNeural` | General |
| English (Hongkong) | `en-HK` | Male | `en-HK-SamNeural` | General |
| English (India) | `en-IN` | Female | `en-IN-NeerjaNeural` | General |
| English (India) | `en-IN` | Male | `en-IN-PrabhatNeural` | General |
| English (Ireland) | `en-IE` | Female | `en-IE-EmilyNeural` | General |
| English (Ireland) | `en-IE` | Male | `en-IE-ConnorNeural` | General |
| English (Kenya) | `en-KE` | Female | `en-KE-AsiliaNeural` <sup>New</sup>  | General |
| English (Kenya) | `en-KE` | Male | `en-KE-ChilembaNeural` <sup>New</sup>  | General |
| English (New Zealand) | `en-NZ` | Female | `en-NZ-MollyNeural` | General |
| English (New Zealand) | `en-NZ` | Male | `en-NZ-MitchellNeural` | General |
| English (Nigeria) | `en-NG` | Female | `en-NG-EzinneNeural` <sup>New</sup>  | General |
| English (Nigeria) | `en-NG` | Male | `en-NG-AbeoNeural` <sup>New</sup>  | General |
| English (Philippines) | `en-PH` | Female | `en-PH-RosaNeural` | General | 
| English (Philippines) | `en-PH` | Male | `en-PH-JamesNeural` | General | 
| English (Singapore) | `en-SG` | Female | `en-SG-LunaNeural` | General |
| English (Singapore) | `en-SG` | Male | `en-SG-WayneNeural` | General |
| English (South Africa) | `en-ZA` | Female | `en-ZA-LeahNeural` | General |
| English (South Africa) | `en-ZA` | Male | `en-ZA-LukeNeural` | General |
| English (Tanzania) | `en-TZ` | Female | `en-TZ-ImaniNeural` <sup>New</sup>  | General |
| English (Tanzania) | `en-TZ` | Male | `en-TZ-ElimuNeural` <sup>New</sup>  | General |
| English (United Kingdom) | `en-GB` | Female | `en-GB-LibbyNeural` | General |
| English (United Kingdom) | `en-GB` | Female | `en-GB-SoniaNeural` | General |
| English (United Kingdom) | `en-GB` | Female | `en-GB-MiaNeural` <sup>Retired on 30 October 2021, see below</sup> | General |
| English (United Kingdom) | `en-GB` | Male | `en-GB-RyanNeural` | General |
| English (United States) | `en-US` | Female | `en-US-AmberNeural` | General |
| English (United States) | `en-US` | Female | `en-US-AriaNeural` | General, multiple voice styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| English (United States) | `en-US` | Female | `en-US-AshleyNeural` | General |
| English (United States) | `en-US` | Female | `en-US-CoraNeural` | General |
| English (United States) | `en-US` | Female | `en-US-ElizabethNeural` | General |
| English (United States) | `en-US` | Female | `en-US-JennyNeural` | General, multiple voice styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| English (United States) | `en-US` | Female | `en-US-MichelleNeural`| General |
| English (United States) | `en-US` | Female | `en-US-MonicaNeural` | General |
| English (United States) | `en-US` | Female | `en-US-SaraNeural` | General, multiple voice styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| English (United States) | `en-US` | Kid | `en-US-AnaNeural`| General |
| English (United States) | `en-US` | Male | `en-US-BrandonNeural` | General |
| English (United States) | `en-US` | Male | `en-US-ChristopherNeural`  | General |
| English (United States) | `en-US` | Male | `en-US-EricNeural` | General |
| English (United States) | `en-US` | Male | `en-US-GuyNeural` | General, multiple voice styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| English (United States) | `en-US` | Male | `en-US-JacobNeural` | General |
| Estonian (Estonia) | `et-EE` | Female | `et-EE-AnuNeural` | General |
| Estonian (Estonia) | `et-EE` | Male | `et-EE-KertNeural` | General |
| Filipino (Philippines) | `fil-PH` | Female | `fil-PH-BlessicaNeural` <sup>New</sup>  | General |
| Filipino (Philippines) | `fil-PH` | Male | `fil-PH-AngeloNeural` <sup>New</sup>  | General |
| Finnish (Finland) | `fi-FI` | Female | `fi-FI-NooraNeural` | General |
| Finnish (Finland) | `fi-FI` | Female | `fi-FI-SelmaNeural` | General |
| Finnish (Finland) | `fi-FI` | Male | `fi-FI-HarriNeural` | General |
| French (Belgium) | `fr-BE` | Female | `fr-BE-CharlineNeural` | General | 
| French (Belgium) | `fr-BE` | Male | `fr-BE-GerardNeural` | General | 
| French (Canada) | `fr-CA` | Female | `fr-CA-SylvieNeural` | General |
| French (Canada) | `fr-CA` | Male | `fr-CA-AntoineNeural` | General |
| French (Canada) | `fr-CA` | Male | `fr-CA-JeanNeural` | General |
| French (France) | `fr-FR` | Female | `fr-FR-DeniseNeural` | General |
| French (France) | `fr-FR` | Male | `fr-FR-HenriNeural` | General |
| French (Switzerland) | `fr-CH` | Female | `fr-CH-ArianeNeural` | General |
| French (Switzerland) | `fr-CH` | Male | `fr-CH-FabriceNeural` | General |
| Galician (Spain) | `gl-ES` | Female | `gl-ES-SabelaNeural` <sup>New</sup>  | General |
| Galician (Spain) | `gl-ES` | Male | `gl-ES-RoiNeural` <sup>New</sup>  | General |
| German (Austria) | `de-AT` | Female | `de-AT-IngridNeural` | General |
| German (Austria) | `de-AT` | Male | `de-AT-JonasNeural` | General |
| German (Germany) | `de-DE` | Female | `de-DE-KatjaNeural` | General |
| German (Germany) | `de-DE` | Male | `de-DE-ConradNeural` | General |
| German (Switzerland) | `de-CH` | Female | `de-CH-LeniNeural` | General |
| German (Switzerland) | `de-CH` | Male | `de-CH-JanNeural` | General |
| Greek (Greece) | `el-GR` | Female | `el-GR-AthinaNeural` | General |
| Greek (Greece) | `el-GR` | Male | `el-GR-NestorasNeural` | General |
| Gujarati (India) | `gu-IN` | Female | `gu-IN-DhwaniNeural` | General |
| Gujarati (India) | `gu-IN` | Male | `gu-IN-NiranjanNeural` | General |
| Hebrew (Israel) | `he-IL` | Female | `he-IL-HilaNeural` | General |
| Hebrew (Israel) | `he-IL` | Male | `he-IL-AvriNeural` | General |
| Hindi (India) | `hi-IN` | Female | `hi-IN-SwaraNeural` | General |
| Hindi (India) | `hi-IN` | Male | `hi-IN-MadhurNeural` | General |
| Hungarian (Hungary) | `hu-HU` | Female | `hu-HU-NoemiNeural` | General |
| Hungarian (Hungary) | `hu-HU` | Male | `hu-HU-TamasNeural` | General |
| Indonesian (Indonesia) | `id-ID` | Female | `id-ID-GadisNeural` | General |
| Indonesian (Indonesia) | `id-ID` | Male | `id-ID-ArdiNeural` | General |
| Irish (Ireland) | `ga-IE` | Female | `ga-IE-OrlaNeural` | General |
| Irish (Ireland) | `ga-IE` | Male | `ga-IE-ColmNeural` | General |
| Italian (Italy) | `it-IT` | Female | `it-IT-ElsaNeural` | General |
| Italian (Italy) | `it-IT` | Female | `it-IT-IsabellaNeural` | General |
| Italian (Italy) | `it-IT` | Male | `it-IT-DiegoNeural` | General |
| Japanese (Japan) | `ja-JP` | Female | `ja-JP-NanamiNeural` | General |
| Japanese (Japan) | `ja-JP` | Male | `ja-JP-KeitaNeural` | General |
| Javanese (Indonesia) | `jv-ID` | Female | `jv-ID-SitiNeural` <sup>New</sup>  | General |
| Javanese (Indonesia) | `jv-ID` | Male | `jv-ID-DimasNeural` <sup>New</sup>  | General |
| Khmer (Cambodia) | `km-KH` | Female | `km-KH-SreymomNeural` <sup>New</sup>  | General |
| Khmer (Cambodia) | `km-KH` | Male | `km-KH-PisethNeural` <sup>New</sup>  | General |
| Korean (Korea) | `ko-KR` | Female | `ko-KR-SunHiNeural` | General |
| Korean (Korea) | `ko-KR` | Male | `ko-KR-InJoonNeural` | General |
| Latvian (Latvia) | `lv-LV` | Female | `lv-LV-EveritaNeural` | General |
| Latvian (Latvia) | `lv-LV` | Male | `lv-LV-NilsNeural` | General |
| Lithuanian (Lithuania) | `lt-LT` | Female | `lt-LT-OnaNeural` | General |
| Lithuanian (Lithuania) | `lt-LT` | Male | `lt-LT-LeonasNeural` | General |
| Malay (Malaysia) | `ms-MY` | Female | `ms-MY-YasminNeural` | General |
| Malay (Malaysia) | `ms-MY` | Male | `ms-MY-OsmanNeural` | General |
| Maltese (Malta) | `mt-MT` | Female | `mt-MT-GraceNeural` | General |
| Maltese (Malta) | `mt-MT` | Male | `mt-MT-JosephNeural` | General |
| Marathi (India) | `mr-IN` | Female | `mr-IN-AarohiNeural` | General |
| Marathi (India) | `mr-IN` | Male | `mr-IN-ManoharNeural` | General |
| Norwegian (Bokmål, Norway) | `nb-NO` | Female | `nb-NO-IselinNeural` | General |
| Norwegian (Bokmål, Norway) | `nb-NO` | Female | `nb-NO-PernilleNeural` | General |
| Norwegian (Bokmål, Norway) | `nb-NO` | Male | `nb-NO-FinnNeural` | General |
| Persian (Iran) | `fa-IR` | Female | `fa-IR-DilaraNeural` <sup>New</sup>  | General |
| Persian (Iran) | `fa-IR` | Male | `fa-IR-FaridNeural` <sup>New</sup>  | General |
| Polish (Poland) | `pl-PL` | Female | `pl-PL-AgnieszkaNeural` | General |
| Polish (Poland) | `pl-PL` | Female | `pl-PL-ZofiaNeural` | General |
| Polish (Poland) | `pl-PL` | Male | `pl-PL-MarekNeural` | General |
| Portuguese (Brazil) | `pt-BR` | Female | `pt-BR-FranciscaNeural` | General, multiple voice styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles) |
| Portuguese (Brazil) | `pt-BR` | Male | `pt-BR-AntonioNeural` | General |
| Portuguese (Portugal) | `pt-PT` | Female | `pt-PT-FernandaNeural` | General |
| Portuguese (Portugal) | `pt-PT` | Female | `pt-PT-RaquelNeural` | General |
| Portuguese (Portugal) | `pt-PT` | Male | `pt-PT-DuarteNeural` | General |
| Romanian (Romania) | `ro-RO` | Female | `ro-RO-AlinaNeural` | General |
| Romanian (Romania) | `ro-RO` | Male | `ro-RO-EmilNeural` | General |
| Russian (Russia) | `ru-RU` | Female | `ru-RU-DariyaNeural` | General |
| Russian (Russia) | `ru-RU` | Female | `ru-RU-SvetlanaNeural` | General |
| Russian (Russia) | `ru-RU` | Male | `ru-RU-DmitryNeural` | General |
| Slovak (Slovakia) | `sk-SK` | Female | `sk-SK-ViktoriaNeural` | General |
| Slovak (Slovakia) | `sk-SK` | Male | `sk-SK-LukasNeural` | General |
| Slovenian (Slovenia) | `sl-SI` | Female | `sl-SI-PetraNeural` | General |
| Slovenian (Slovenia) | `sl-SI` | Male | `sl-SI-RokNeural` | General |
| Somali (Somalia) | `so-SO` | Female | `so-SO-UbaxNeural` <sup>New</sup>  | General |
| Somali (Somalia) | `so-SO`| Male | `so-SO-MuuseNeural` <sup>New</sup>  | General |
| Spanish (Argentina) | `es-AR` | Female | `es-AR-ElenaNeural` | General |
| Spanish (Argentina) | `es-AR` | Male | `es-AR-TomasNeural` | General |
| Spanish (Bolivia) | `es-BO` | Female | `es-BO-SofiaNeural` <sup>New</sup>  | General |
| Spanish (Bolivia) | `es-BO` | Male | `es-BO-MarceloNeural` <sup>New</sup>  | General |
| Spanish (Chile) | `es-CL` | Female | `es-CL-CatalinaNeural` <sup>New</sup>  | General |
| Spanish (Chile) | `es-CL` | Male | `es-CL-LorenzoNeural` <sup>New</sup>  | General |
| Spanish (Colombia) | `es-CO` | Female | `es-CO-SalomeNeural` | General |
| Spanish (Colombia) | `es-CO` | Male | `es-CO-GonzaloNeural` | General |
| Spanish (Costa Rica) | `es-CR` | Female | `es-CR-MariaNeural` <sup>New</sup>  | General |
| Spanish (Costa Rica) | `es-CR` | Male | `es-CR-JuanNeural` <sup>New</sup>  | General |
| Spanish (Cuba) | `es-CU` | Female | `es-CU-BelkysNeural` <sup>New</sup>  | General |
| Spanish (Cuba) | `es-CU` | Male | `es-CU-ManuelNeural` <sup>New</sup>  | General |
| Spanish (Dominican Republic) | `es-DO` | Female | `es-DO-RamonaNeural` <sup>New</sup>  | General |
| Spanish (Dominican Republic) | `es-DO` | Male | `es-DO-EmilioNeural` <sup>New</sup>  | General |
| Spanish (Ecuador) | `es-EC` | Female | `es-EC-AndreaNeural` <sup>New</sup>  | General |
| Spanish (Ecuador) | `es-EC` | Male | `es-EC-LuisNeural` <sup>New</sup>  | General |
| Spanish (El Salvador) | `es-SV` | Female | `es-SV-LorenaNeural` <sup>New</sup>  | General |
| Spanish (El Salvador) | `es-SV` | Male | `es-SV-RodrigoNeural` <sup>New</sup>  | General |
| Spanish (Equatorial Guinea) | `es-GQ` | Female | `es-GQ-TeresaNeural` <sup>New</sup>  | General |
| Spanish (Equatorial Guinea) | `es-GQ` | Male | `es-GQ-JavierNeural` <sup>New</sup>  | General |
| Spanish (Guatemala) | `es-GT` | Female | `es-GT-MartaNeural` <sup>New</sup>  | General |
| Spanish (Guatemala) | `es-GT` | Male | `es-GT-AndresNeural` <sup>New</sup>  | General |
| Spanish (Honduras) | `es-HN` | Female | `es-HN-KarlaNeural` <sup>New</sup>  | General |
| Spanish (Honduras) | `es-HN` | Male | `es-HN-CarlosNeural` <sup>New</sup>  | General |
| Spanish (Mexico) | `es-MX` | Female | `es-MX-DaliaNeural` | General |
| Spanish (Mexico) | `es-MX` | Male | `es-MX-JorgeNeural` | General |
| Spanish (Nicaragua) | `es-NI` | Female | `es-NI-YolandaNeural` <sup>New</sup>  | General |
| Spanish (Nicaragua) | `es-NI` | Male | `es-NI-FedericoNeural` <sup>New</sup>  | General |
| Spanish (Panama) | `es-PA` | Female | `es-PA-MargaritaNeural` <sup>New</sup>  | General |
| Spanish (Panama) | `es-PA` | Male | `es-PA-RobertoNeural` <sup>New</sup>  | General |
| Spanish (Paraguay) | `es-PY` | Female | `es-PY-TaniaNeural` <sup>New</sup>  | General |
| Spanish (Paraguay) | `es-PY` | Male | `es-PY-MarioNeural` <sup>New</sup>  | General |
| Spanish (Peru) | `es-PE` | Female | `es-PE-CamilaNeural` <sup>New</sup>  | General |
| Spanish (Peru) | `es-PE` | Male | `es-PE-AlexNeural` <sup>New</sup>  | General |
| Spanish (Puerto Rico) | `es-PR` | Female | `es-PR-Karina Neural` <sup>New</sup>  | General |
| Spanish (Puerto Rico) | `es-PR` | Male | `es-PR-Victor Neural` <sup>New</sup>  | General |
| Spanish (Spain) | `es-ES` | Female | `es-ES-ElviraNeural` | General |
| Spanish (Spain) | `es-ES` | Male | `es-ES-AlvaroNeural` | General |
| Spanish (Uruguay) | `es-UY` | Female | `es-UY-ValentinaNeural` <sup>New</sup>  | General |
| Spanish (Uruguay) | `es-UY` | Male | `es-UY-MateoNeural` <sup>New</sup>  | General |
| Spanish (US) | `es-US` | Female | `es-US-PalomaNeural` | General |
| Spanish (US) | `es-US` | Male | `es-US-AlonsoNeural` | General |
| Spanish (Venezuela) | `es-VE` | Female | `es-VE-PaolaNeural` <sup>New</sup>  | General |
| Spanish (Venezuela) | `es-VE` | Male | `es-VE-SebastianNeural` <sup>New</sup>  | General |
| Sundanese (Indonesia) | `su-ID` | Female | `su-ID-TutiNeural` <sup>New</sup>  | General |
| Sundanese (Indonesia) | `su-ID` | Male | `su-ID-JajangNeural` <sup>New</sup>  | General |
| Swahili (Kenya) | `sw-KE` | Female | `sw-KE-ZuriNeural` | General |
| Swahili (Kenya) | `sw-KE` | Male | `sw-KE-RafikiNeural` | General |
| Swahili (Tanzania) | `sw-TZ` | Female | `sw-TZ-RehemaNeural` <sup>New</sup>  | General |
| Swahili (Tanzania) | `sw-TZ` | Male | `sw-TZ-DaudiNeural` <sup>New</sup>  | General |
| Swedish (Sweden) | `sv-SE` | Female | `sv-SE-HilleviNeural` | General |
| Swedish (Sweden) | `sv-SE` | Female | `sv-SE-SofieNeural` | General |
| Swedish (Sweden) | `sv-SE` | Male | `sv-SE-MattiasNeural` | General |
| Tamil (India) | `ta-IN` | Female | `ta-IN-PallaviNeural` | General |
| Tamil (India) | `ta-IN` | Male | `ta-IN-ValluvarNeural` | General |
| Tamil (Singapore) | `ta-SG` | Female | `ta-SG-VenbaNeural` <sup>New</sup>  | General |
| Tamil (Singapore) | `ta-SG` | Male | `ta-SG-AnbuNeural` <sup>New</sup>  | General |
| Tamil (Sri Lanka) | `ta-LK` | Female | `ta-LK-SaranyaNeural` <sup>New</sup>  | General |
| Tamil (Sri Lanka) | `ta-LK` | Male | `ta-LK-KumarNeural` <sup>New</sup>  | General |
| Telugu (India) | `te-IN` | Female | `te-IN-ShrutiNeural` | General |
| Telugu (India) | `te-IN` | Male | `te-IN-MohanNeural` | General |
| Thai (Thailand) | `th-TH` | Female | `th-TH-AcharaNeural` | General |
| Thai (Thailand) | `th-TH` | Female | `th-TH-PremwadeeNeural` | General |
| Thai (Thailand) | `th-TH` | Male | `th-TH-NiwatNeural` | General |
| Turkish (Turkey) | `tr-TR` | Female | `tr-TR-EmelNeural` | General |
| Turkish (Turkey) | `tr-TR` | Male | `tr-TR-AhmetNeural` | General |
| Ukrainian (Ukraine) | `uk-UA` | Female | `uk-UA-PolinaNeural` | General | 
| Ukrainian (Ukraine) | `uk-UA` | Male | `uk-UA-OstapNeural` | General | 
| Urdu (India) | `ur-IN` | Female | `ur-IN-GulNeural` <sup>New</sup>  | General |
| Urdu (India) | `ur-IN` | Male | `ur-IN-SalmanNeural` <sup>New</sup>  | General |
| Urdu (Pakistan) | `ur-PK` | Female | `ur-PK-UzmaNeural`  | General | 
| Urdu (Pakistan) | `ur-PK` | Male | `ur-PK-AsadNeural` | General | 
| Uzbek (Uzbekistan) | `uz-UZ` | Female | `uz-UZ-MadinaNeural` <sup>New</sup>  | General |
| Uzbek (Uzbekistan) | `uz-UZ` | Male | `uz-UZ-SardorNeural` <sup>New</sup>  | General |
| Vietnamese (Vietnam) | `vi-VN` | Female | `vi-VN-HoaiMyNeural` | General |
| Vietnamese (Vietnam) | `vi-VN` | Male | `vi-VN-NamMinhNeural` | General |
| Welsh (United Kingdom) | `cy-GB` | Female | `cy-GB-NiaNeural` | General | 
| Welsh (United Kingdom) | `cy-GB` | Male | `cy-GB-AledNeural` | General | 
| Zulu (South Africa) | `zu-ZA` | Female | `zu-ZA-ThandoNeural` <sup>New</sup>  | General |
| Zulu (South Africa) | `zu-ZA` | Male | `zu-ZA-ThembaNeural` <sup>New</sup>  | General |

> [!IMPORTANT]
> The English (United Kingdom) voice `en-GB-MiaNeural` retired on **30 October 2021**. All service requests to `en-GB-MiaNeural` now will be re-directed to `en-GB-SoniaNeural` automatically since **30 October 2021**.
> If you are using container Neural TTS, please [download](speech-container-howto.md#get-the-container-image-with-docker-pull) and deploy the latest version, starting from **30 October 2021**, all requests with previous versions will be rejected.

#### Neural voices in preview

Below neural voices are in public preview. 

| Language                         | Locale  | Gender | Voice name                             | Style support |
|----------------------------------|---------|--------|----------------------------------------|---------------|
| English (United States) | `en-US` | Female | `en-US-JennyMultilingualNeural` <sup>New</sup> | General，multi-lingual capabilities available [using SSML](speech-synthesis-markup.md#create-an-ssml-document) |
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaochenNeural` <sup>New</sup> | Optimized for spontaneous conversation |
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaoyanNeural` <sup>New</sup> | Optimized for customer service |
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaoshuangNeural` <sup>New</sup> | Child voice，optimized for child story and chat; multiple voice styles available [using SSML](speech-synthesis-markup.md#adjust-speaking-styles)|
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-XiaoqiuNeural` <sup>New</sup> | Optimized for narrating |

> [!IMPORTANT]
> Voices in public preview are only available in 3 service regions: East US, West Europe and Southeast Asia.

> [!TIP]
> `en-US-JennyNeuralMultilingual` supports multiple languages. Check the [voices list API](rest-text-to-speech.md#get-a-list-of-voices) for supported languages list.

For more information about regional availability, see [regions](regions.md#neural-and-standard-voices).

To learn how you can configure and adjust neural voices, such as Speaking Styles, see [Speech Synthesis Markup Language](speech-synthesis-markup.md#adjust-speaking-styles).

> [!IMPORTANT]
> The `en-US-JessaNeural` voice has changed to `en-US-AriaNeural`. If you were using "Jessa" before, convert over to "Aria".

> [!TIP]
> You can continue to use the full service name mapping like "Microsoft Server Speech Text to Speech Voice (en-US, ChristopherNeural)" in your speech synthesis requests.

### Standard voices

More than 75 standard voices are available in over 45 languages and locales, which allow you to convert text into synthesized speech. For more information about regional availability, see [regions](regions.md#neural-and-standard-voices).

> [!IMPORTANT]
> We are retiring the standard voices on **31st August 2024** and they will no longer be supported after that date. We announced this in emails sent to all existing Speech subscriptions created before **31st August 2021**. During the retiring period (**31st August 2021** - **31st August 2024**), existing standard voice users can continue to use standard voices, but all new users/new speech resources must choose neural voices.

> [!NOTE]
> With two exceptions, standard voices are created from samples that use a 16 khz sample rate.
> **The en-US-AriaRUS** and **en-US-GuyRUS** voices are also created from samples that use a 24 khz sample rate.
> All voices can upsample or downsample to other sample rates when synthesizing.

| Language | Locale (BCP-47) | Gender | Voice name |
|--|--|--|--|
| Arabic (Egypt) | `ar-EG` | Female | `ar-EG-Hoda`|
| Arabic (Saudi Arabia) | `ar-SA` | Male | `ar-SA-Naayf`|
| Bulgarian (Bulgaria) | `bg-BG` | Male | `bg-BG-Ivan`|
| Catalan (Spain) | `ca-ES` | Female | `ca-ES-HerenaRUS`|
| Chinese (Cantonese, Traditional) | `zh-HK` | Male | `zh-HK-Danny`|
| Chinese (Cantonese, Traditional) | `zh-HK` | Female | `zh-HK-TracyRUS`|
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-HuihuiRUS`|
| Chinese (Mandarin, Simplified) | `zh-CN` | Male | `zh-CN-Kangkang`|
| Chinese (Mandarin, Simplified) | `zh-CN` | Female | `zh-CN-Yaoyao`|
| Chinese (Taiwanese Mandarin) |  `zh-TW` | Female | `zh-TW-HanHanRUS`|
| Chinese (Taiwanese Mandarin) |  `zh-TW` | Female | `zh-TW-Yating`|
| Chinese (Taiwanese Mandarin) |  `zh-TW` | Male | `zh-TW-Zhiwei`|
| Croatian (Croatia) | `hr-HR` | Male | `hr-HR-Matej`|
| Czech (Czech) | `cs-CZ` | Male | `cs-CZ-Jakub`|
| Danish (Denmark) | `da-DK` | Female | `da-DK-HelleRUS`|
| Dutch (Netherlands) | `nl-NL` | Female | `nl-NL-HannaRUS`|
| English (Australia) | `en-AU` | Female | `en-AU-Catherine`|
| English (Australia) | `en-AU` | Female | `en-AU-HayleyRUS`|
| English (Canada) | `en-CA` | Female | `en-CA-HeatherRUS`|
| English (Canada) | `en-CA` | Female | `en-CA-Linda`|
| English (India) | `en-IN` | Female | `en-IN-Heera`|
| English (India) | `en-IN` | Female | `en-IN-PriyaRUS`|
| English (India) | `en-IN` | Male | `en-IN-Ravi`|
| English (Ireland) | `en-IE` | Male | `en-IE-Sean`|
| English (United Kingdom) | `en-GB` | Male | `en-GB-George`|
| English (United Kingdom) | `en-GB` | Female | `en-GB-HazelRUS`|
| English (United Kingdom) | `en-GB` | Female | `en-GB-Susan`|
| English (United States) | `en-US` | Male | `en-US-BenjaminRUS`|
| English (United States) | `en-US` | Male | `en-US-GuyRUS`|
| English (United States) | `en-US` | Female | `en-US-AriaRUS`|
| English (United States) | `en-US` | Female | `en-US-ZiraRUS`|
| Finnish (Finland) | `fi-FI` | Female | `fi-FI-HeidiRUS`|
| French (Canada) | `fr-CA` | Female | `fr-CA-Caroline`|
| French (Canada) | `fr-CA` | Female | `fr-CA-HarmonieRUS`|
| French (France) | `fr-FR` | Female | `fr-FR-HortenseRUS`|
| French (France) | `fr-FR` | Female | `fr-FR-Julie`|
| French (France) | `fr-FR` | Male | `fr-FR-Paul`|
| French (Switzerland) | `fr-CH` | Male | `fr-CH-Guillaume`|
| German (Austria) | `de-AT` | Male | `de-AT-Michael`|
| German (Germany) | `de-DE` | Female | `de-DE-HeddaRUS`|
| German (Germany) | `de-DE` | Male | `de-DE-Stefan`|
| German (Switzerland) | `de-CH` | Male | `de-CH-Karsten`|
| Greek (Greece) | `el-GR` | Male | `el-GR-Stefanos`|
| Hebrew (Israel) | `he-IL` | Male | `he-IL-Asaf`|
| Hindi (India) | `hi-IN` | Male | `hi-IN-Hemant`|
| Hindi (India) | `hi-IN` | Female | `hi-IN-Kalpana`|
| Hungarian (Hungary) | `hu-HU` | Male | `hu-HU-Szabolcs`|
| Indonesian (Indonesia) | `id-ID` | Male | `id-ID-Andika`|
| Italian (Italy) | `it-IT` | Male | `it-IT-Cosimo`|
| Italian (Italy) | `it-IT` | Female | `it-IT-LuciaRUS`|
| Japanese (Japan) | `ja-JP` | Female | `ja-JP-Ayumi`|
| Japanese (Japan) | `ja-JP` | Female | `ja-JP-HarukaRUS`|
| Japanese (Japan) | `ja-JP` | Male | `ja-JP-Ichiro`|
| Korean (Korea) | `ko-KR` | Female | `ko-KR-HeamiRUS`|
| Malay (Malaysia) | `ms-MY` | Male | `ms-MY-Rizwan`|
| Norwegian (Bokmål, Norway) | `nb-NO` | Female | `nb-NO-HuldaRUS`|
| Polish (Poland) | `pl-PL` | Female | `pl-PL-PaulinaRUS`|
| Portuguese (Brazil) | `pt-BR` | Male | `pt-BR-Daniel`|
| Portuguese (Brazil) | `pt-BR` | Female | `pt-BR-HeloisaRUS`|
| Portuguese (Portugal) | `pt-PT` | Female | `pt-PT-HeliaRUS`|
| Romanian (Romania) | `ro-RO` | Male | `ro-RO-Andrei`|
| Russian (Russia) | `ru-RU` | Female | `ru-RU-EkaterinaRUS`|
| Russian (Russia) | `ru-RU` | Female | `ru-RU-Irina`|
| Russian (Russia) | `ru-RU` | Male | `ru-RU-Pavel`|
| Slovak (Slovakia) | `sk-SK` | Male | `sk-SK-Filip`|
| Slovenian (Slovenia) | `sl-SI` | Male | `sl-SI-Lado`|
| Spanish (Mexico) | `es-MX` | Female | `es-MX-HildaRUS`|
| Spanish (Mexico) | `es-MX` | Male | `es-MX-Raul`|
| Spanish (Spain) | `es-ES` | Female | `es-ES-HelenaRUS`|
| Spanish (Spain) | `es-ES` | Female | `es-ES-Laura`|
| Spanish (Spain) | `es-ES` | Male | `es-ES-Pablo`|
| Swedish (Sweden) | `sv-SE` | Female | `sv-SE-HedvigRUS`|
| Tamil (India) | `ta-IN` | Male | `ta-IN-Valluvar`|
| Telugu (India) | `te-IN` | Female | `te-IN-Chitra`|
| Thai (Thailand) | `th-TH` | Male | `th-TH-Pattara`|
| Turkish (Turkey) | `tr-TR` | Female | `tr-TR-SedaRUS`|
| Vietnamese (Vietnam) | `vi-VN` | Male | `vi-VN-An` |

> [!IMPORTANT]
> The `en-US-Jessa` voice has changed to `en-US-Aria`. If you were using "Jessa" before, convert over to "Aria".

> [!TIP]
> You can continue to use the full service name mapping like "Microsoft Server Speech Text to Speech Voice (en-US, AriaRUS)" in your speech synthesis requests.

### Customization

Custom Voice is available in the neural tier (a.k.a, Custom Neural Voice). Based on the Neural TTS technology and the multi-lingual multi-speaker universal model, Custom Neural Voice lets you create synthetic voices that are rich in speaking styles, or adaptable cross languages. Check below for the languages supported.  

> [!IMPORTANT]
> The standard tier including the statistical parametric and the concatenative training methods of custom voice is being deprecated and will be retired on 2/29/2024. If you are using non-neural/standard Custom Voice, migrate to Custom Neural Voice immediately to enjoy the better quality and deploy the voices responsibly. 

| Language | Locale | Neural | Cross-lingual |
|--|--|--|--|
| Arabic (Egypt) | `ar-EG` | Yes | No |
| Bulgarian (Bulgaria) | `bg-BG` | Yes | No |
| Chinese (Mandarin, Simplified) | `zh-CN` | Yes | Yes |
| Chinese (Mandarin, Simplified), English bilingual | `zh-CN` bilingual | Yes | Yes |
| Chinese (Taiwanese Mandarin) | `zh-TW` | Yes | No |
| Czech (Czech) | `cs-CZ` | Yes | No |
| Dutch (Netherlands) | `nl-NL` | Yes | No |
| English (Australia) | `en-AU` | Yes | Yes |
| English (Canada) | `en-CA` | Yes | No |
| English (India) | `en-IN` | Yes | No |
| English (Ireland) | `en-IE` | Yes | No |
| English (United Kingdom) | `en-GB` | Yes | Yes |
| English (United States) | `en-US` | Yes | Yes |
| French (Canada) | `fr-CA` | Yes | Yes |
| French (France) | `fr-FR` | Yes | Yes |
| German (Austria) | `de-AT` | Yes | No |
| German (Germany) | `de-DE` | Yes | Yes |
| Hungarian (Hungary) | `hu-HU` | Yes | No |
| Italian (Italy) | `it-IT` | Yes | Yes |
| Japanese (Japan) | `ja-JP` | Yes | Yes |
| Korean (Korea) | `ko-KR` | Yes | Yes |
| Norwegian (Bokmål, Norway) | `nb-NO` | Yes | No |
| Portuguese (Brazil) | `pt-BR` | Yes | Yes |
| Portuguese (Portugal) | `pt-PT` | Yes | No |
| Russian (Russia) | `ru-RU` | Yes | Yes |
| Slovak (Slovakia) | `sk-SK` | Yes | No |
| Spanish (Mexico) | `es-MX` | Yes | Yes |
| Spanish (Spain) | `es-ES` | Yes | Yes |
| Turkish (Turkey) | `tr-TR` | Yes | No |
| Vietnamese (Vietnam) | `vi-VN` | Yes | No |

Select the right locale that matches the training data you have to train a custom voice model. For example, if the recording data you have is spoken in English with a British accent, select `en-GB`.

> [!NOTE]
> We do not support bi-lingual model training in Custom Voice, except for the Chinese-English bi-lingual. Select "Chinese-English bilingual" if you want to train a Chinese voice that can speak English as well. Chinese-English bilingual model training using the standard method is available in North Europe and North Central US only. Custom Neural Voice training is available in UK South and East US.

## Speech translation

The **Speech Translation** API supports different languages for speech-to-speech and speech-to-text translation. The source language must always be from the Speech-to-text language table. The available target languages depend on whether the translation target is speech or text. You may translate incoming speech into any of the  [supported languages](https://www.microsoft.com/translator/business/languages/). A subset of languages are available for [speech synthesis](language-support.md#text-languages).

### Text languages

| Text language           | Language code |
|:------------------------|:-------------:|
| Afrikaans | `af` |
| Albanian | `sq` |
| Amharic | `am` |
| Arabic | `ar` |
| Armenian | `hy` |
| Assamese | `as` |
| Azerbaijani | `az` |
| Bangla | `bn` |
| Bosnian (Latin) | `bs` |
| Bulgarian | `bg` |
| Cantonese (Traditional) | `yue` |
| Catalan | `ca` |
| Chinese (Literary) | `lzh` |
| Chinese Simplified | `zh-Hans` |
| Chinese Traditional | `zh-Hant` |
| Croatian | `hr` |
| Czech | `cs` |
| Danish | `da` |
| Dari | `prs` |
| Dutch | `nl` |
| English | `en` |
| Estonian | `et` |
| Fijian | `fj` |
| Filipino | `fil` |
| Finnish | `fi` |
| French | `fr` |
| French (Canada) | `fr-ca` |
| German | `de` |
| Greek | `el` |
| Gujarati | `gu` |
| Haitian Creole | `ht` |
| Hebrew | `he` |
| Hindi | `hi` |
| Hmong Daw | `mww` |
| Hungarian | `hu` |
| Icelandic | `is` |
| Indonesian | `id` |
| Inuktitut | `iu` |
| Irish | `ga` |
| Italian | `it` |
| Japanese | `ja` |
| Kannada | `kn` |
| Kazakh | `kk` |
| Khmer | `km` |
| Klingon | `tlh-Latn` |
| Klingon (plqaD) | `tlh-Piqd` |
| Korean | `ko` |
| Kurdish (Central) | `ku` |
| Kurdish (Northern) | `kmr` |
| Lao | `lo` |
| Latvian | `lv` |
| Lithuanian | `lt` |
| Malagasy | `mg` |
| Malay | `ms` |
| Malayalam | `ml` |
| Maltese | `mt` |
| Maori | `mi` |
| Marathi | `mr` |
| Myanmar | `my` |
| Nepali | `ne` |
| Norwegian | `nb` |
| Odia | `or` |
| Pashto | `ps` |
| Persian | `fa` |
| Polish | `pl` |
| Portuguese (Brazil) | `pt` |
| Portuguese (Portugal) | `pt-pt` |
| Punjabi | `pa` |
| Queretaro Otomi | `otq` |
| Romanian | `ro` |
| Russian | `ru` |
| Samoan | `sm` |
| Serbian (Cyrillic) | `sr-Cyrl` |
| Serbian (Latin) | `sr-Latn` |
| Slovak | `sk` |
| Slovenian | `sl` |
| Spanish | `es` |
| Swahili | `sw` |
| Swedish | `sv` |
| Tahitian | `ty` |
| Tamil | `ta` |
| Telugu | `te` |
| Thai | `th` |
| Tigrinya | `ti` |
| Tongan | `to` |
| Turkish | `tr` |
| Ukrainian | `uk` |
| Urdu | `ur` |
| Vietnamese | `vi` |
| Welsh | `cy` |
| Yucatec Maya | `yua` |

## Speaker Recognition

Speaker recognition is mostly language agnostic. We built a universal model for text-independent speaker recognition by combining various data sources from multiple languages. We have tuned and evaluated the model on the languages and locales that appear in the following table. See the [overview](speaker-recognition-overview.md) for additional information on Speaker Recognition.

| Language | Locale (BCP-47) | Text-dependent verification | Text-independent verification | Text-independent identification |
|----|----|----|----|----|
|English (US)  |  `en-US`  |  yes  |  yes  |  yes |
|Chinese (Mandarin, simplified) | `zh-CN`     |     n/a |     yes |     yes|
|English (Australia)     | `en-AU`    | n/a     | yes     | yes|
|English (Canada)     | `en-CA`     | n/a |     yes |     yes|
|English (India)     | `en-IN`     | n/a |     yes |     yes|
|English (UK)     | `en-GB`     | n/a     | yes     | yes|
|French (Canada)     | `fr-CA`     | n/a     | yes |     yes|
|French (France)     | `fr-FR`     | n/a     | yes     | yes|
|German (Germany)     | `de-DE`     | n/a     | yes     | yes|
|Italian | `it-IT`     |     n/a     | yes |     yes|
|Japanese     | `ja-JP` | n/a     | yes     | yes|
|Portuguese (Brazil) | `pt-BR` |     n/a |     yes |     yes|
|Spanish (Mexico)     | `es-MX`     | n/a |     yes |     yes|
|Spanish (Spain)     | `es-ES` | n/a     | yes |     yes|

## Custom Keyword and Keyword Verification

The following table outlines supported languages for Custom Keyword and Keyword Verification.

| Language | Locale (BCP-47) | Custom Keyword | Keyword Verification |
| -------- | --------------- | -------------- | -------------------- |
| Chinese (Mandarin, Simplified) | zh-CN | Yes | Yes |
| English (United States) | en-US | Yes | Yes |
| Japanese (Japan) | ja-JP | No | Yes |
| Portuguese (Brazil) | pt-BR | No | Yes |

## Next steps

* [Create a free Azure account](https://azure.microsoft.com/free/cognitive-services/)
* [See how to recognize speech in C#](./get-started-speech-to-text.md?pivots=programming-language-chsarp)
