# 4. Hafta: Deney Kurulumu ve Yürütme

## Genel Bakış

Artık hem baseline (ReAct-style) agent hem de Deep Agent çalışır durumda ve UI'a bağlı olduğuna göre, araştırma projesinin kalbi olan ampirik deneylere geçebiliriz.

Bu hafta her iki agent'ı da **SWE-QA benchmark** üzerinde çalıştırarak performanslarını, reasoning süreçlerini ve verimliliklerini karşılaştıracaksınız.

Her zamanki gibi, otomasyon script'lerini hızlı ve hatasız yazabilmek için LangChain Docs MCP ve DeepWiki MCP'ye bağlı "Vibe-Coding" araçlarınızı kullanmayı unutmayın.

## Deney Konfigürasyonları

İki farklı mimariyi SWE-QA soruları üzerinde karşılaştıracaksınız:

### 1. Baseline Agent (ReAct-style)
- **Araçlar:** Kesinlikle sadece orijinal SWE-QA paper'ındaki üç araçla sınırlı kalmalıdır: `read_file`, `get_repo_structure`, ve `search_rag`.
- **Mimari:** Standart LangChain `create_agent()` yapısı kullanılarak oluşturulan standart multi-step reasoning mimarisi. Görevleri sadece RAG ve dosya okuma araçlarıyla çözer.

### 2. Deep Agent
- **Araçlar:** Kendi orijinal, varsayılan araç setini (sanal dosya sistemi vb. dahil) kullanır.
- **KRİTİK System Prompt Güncellemesi:** Deep Agent'ın **System Prompt**'unu değiştirmelisiniz. Agent'a, her soru veya görev için planlama yapmak adına **MUTLAKA** bir **TODO list** kullanmasını ve görevi tamamlamak için **MUTLAKA** "generic sub-agent"i (LangChain Deep Agents kütüphanesinde varsayılan olarak bulunur) kullanmasını kesin bir dille belirtmelisiniz.
- **Mimari:** Hiyerarşik görev dağıtımı (task decomposition). Kod anlama görevlerini bir sub-agent'a devretmenin, standart ReAct yapısından daha iyi olup olmadığını test edeceğiz.

## Yürütme Kuralları

Bilimsel geçerliliği korumak ve verilerin birbirine karışmasını önlemek için aşağıdaki yürütme kurallarına kesinlikle uymalısınız:

### 1. Kesin Context İzolasyonu (Tek Tek Sorulmalı)
Agent'lar SWE-QA sorularını **tek tek** cevaplamalıdır.
- System prompt tüm sorular boyunca sabit kalmalıdır.
- Ancak, **her soru TAMAMEN yeni ve temiz bir context (yeni bir thread) içinde sorulmalıdır.**
- Asla birden fazla soruyu aynı konuşma (thread) içinde art arda sormayın. Her soru için yeni bir thread başlatmak, bir önceki kod tabanı bilgisinin yeni soruyu bozmasını veya ona yardımcı olmasını engeller.

### 2. Kapsamlı Log Saklama (Kritik Gereksinim)
Bu araştırmanın analiz aşaması sadece nihai sonuca değil, execution trace'lerine (yürütme loglarına) dayanır. LangGraph framework'ü tarafından soru cevaplanırken üretilen **TÜM agent loglarını saklamanız zorunludur**.
- SWE-QA veri setinde cevaplanan her soru için; sistemdeki tüm araç çağrılarını, planner adımlarını, sub-agent eylemlerini ve iç muhakeme adımlarını (reasoning steps) kaydetmelisiniz.
- Bu logları diskinizde düzenli bir şekilde tutmalısınız (örneğin; `question_id` ve `agent_type`'a göre gruplanmış JSON dosyaları halinde).
- Gelecek haftalarda bu logları kullanarak ReAct ve Deep Agent süreçlerinin artılarını ve eksilerini görmek için Error Taxonomy analizi (kalitatif analiz) yapacağız. Eğer raw (ham) logları kaydetmezseniz, deneyleri baştan yapmak zorunda kalırsınız.

### 3. Kesin Sanal Dosya Sistemi (Virtual Filesystem) İzolasyonu
Bir soru için agent'a ortam hazırlarken, agent'ın sanal dosya sistemi (virtual filesystem) **SADECE** o soruyla ilgili kod repository'sini içermelidir.
- Agent'ın aynı anda birden fazla repository'e erişimi olması **KABUL EDİLEMEZ VE ARAŞTIRMA METODOLOJİNİZİ GEÇERSİZ KILAR.** Örneğin; soru Repository A ile ilgiliyse, Repository B ve Repository C agent'ın dosya sisteminde **asla** bulunmamalıdır.
- LLM'in prompt olarak aldığı her soru, sadece ve sadece o sorunun cevabı için gereken ortama sahip olmalıdır. Ne eksik, ne fazla.

## 💰 Maliyet Yönetimi & LLM Seçimi

Tüm SWE-QA veri setini çalıştırmak binlerce sorudan oluşur ve çok fazla LLM kredisi harcar. Deneylerin yarısında kredinizin bitmesini önlemek için:
- **Fon Kaynakları:** Öğrenci paketleriniz aracılığıyla elde ettiğiniz ücretsiz **Google Cloud Vertex AI** ve **Azure Foundry** kredilerinizi kullanmalısınız.
- **Model Seçimi:** Pahalı, üst düzey modeller kullanırsanız bu krediler **yeterli olmayacaktır**. Deneyleri çalıştırırken **orta fiyatlı veya ucuz modeller** (örneğin `GPT-OSS-120B`, `Gemini 3 Flash` vb.) seçmelisiniz.
- **Çalıştırma Stratejisi:** İşe ilk olarak tüm SWE-QA veri setini her iki agent mimarisinde de çalıştırmak için **tek bir LLM** kullanarak başlayın. Bu sayede makaleniz için elinizde en az bir tane tamamlanmış sonuç seti olması garanti altına alınır. Eğer projenin sonunda hala krediniz kalırsa, bulgularınızı güçlendirmek için diğer LLM'leri test edebilirsiniz.

## Bu Haftanın Görevleri

1. **Deep Agent Promptunu Güncelleyin:** Yukarıda anlatıldığı gibi Deep Agent'ın system prompt'unu TODO list ve generic sub-agent kullanımını zorunlu tutacak şekilde değiştirin.
2. **Otomasyon Script'i Yazın:** SWE-QA veri seti üzerinde döngü yapacak bir script yazmak için AI araçlarınızı kullanın.
3. **Çalıştırın ve Loglayın:** Yazdığınız script, soruları hem Baseline Agent'a hem de Deep Agent'a göndermeli (izole thread'ler halinde). Script'in her bir soru için hem agent'ın verdiği final cevabını hem de tüm framework loglarını diske mutlaka kaydettiğinden emin olun.

## Başarı Kriterleri

Gelecek toplantımıza kadar şunları bitirmiş olmalısınız:
1. SWE-QA veri setini her iki agent ile çalıştırabilen otomatik bir script.
2. Veri setinin pilot denemesinin (küçük çaplı ilk tur testinin) tamamlanması.
3. Her bir soru için agent mimarisine göre ayrılmış tam yürütme (execution) loglarını ve nihai cevapları içeren, düzenli olarak klasörlenmiş bir veri seti.

## Gelecek Hafta Ne Olacak?

Önümüzdeki hafta size sonuçları nasıl değerlendireceğinizi ve analiz edeceğinizi anlatan yeni bir metodoloji belgesi verilecek. Ancak elinizde veri olmadan o aşamaya geçemeyiz. Bu yüzden bir sonraki toplantımıza kadar tek önceliğiniz **tüm deneyleri bitirmek** ve **bütün logları çok temiz ve düzenli bir formatta saklamaktır**.

---

## ⚠️ Kritik Uyarılar ve Cezalar

Bu ampirik çalışmanın bilimsel dürüstlüğünü sağlamak için metodolojiye kesinlikle uyulması şarttır. **Aşağıdakilerden herhangi birinin gerçekleşmesi durumunda not cezası alacaksınız:**

1. **Eksik Loglar:** Eğer framework tarafından üretilen yürütme loglarının tamamını saklamayı unutursanız.
2. **Kötü Log Düzeni:** Eğer loglar temiz ve uygun bir şekilde saklanmazsa (örneğin; hangi agent adımlarının ve tool call'ların hangi spesifik SWE-QA sorusuna ait olduğu belli değilse).
3. **Deep Agent Protokol İhlali:** Eğer Deep Agent varsayılan (default) araçları haricinde herhangi bir ekstra araca sahipse veya *tüm* senaryolarda soru çözerken/planlama yaparken TODO listesini ve sub-agent'ları kullanmazsa.
4. **Baseline Agent Protokol İhlali:** Eğer ReAct (baseline) agent, SWE-QA paper'ında kesin olarak belirtilen minimum araç seti dışında herhangi bir ekstra araca sahipse.
5. **Context/Thread Sızıntısı:** Benchmarking (soru testleri) sırasında, gönderilen her yeni prompt ve soru için tamamen yeni ve temiz bir thread oluşturulmazsa.
