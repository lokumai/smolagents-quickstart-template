# 5. Hafta: Değerlendirme ve Analiz Yönergeleri

## 1. Proje Özeti: Aslında neyi araştırıyoruz?

Değerlendirme metriklerine ve loglarınızı nasıl işleyeceğinize geçmeden önce, bitirme projemizin temel hedefini kısaca hatırlayalım.

Amacımız, repository düzeyinde Soru-Cevap (QnA) işlemleri için bir **ReAct Agent** ile bir **Deep Agent**'ı karşılaştırmak ve bu ampirik bulguları bilimsel bir makalede yayımlamaktır.

Bunu başarmak için her iki agent mimarisini **SWE-QA veri seti** üzerinde çalıştırdınız, tüm yürütme (execution) loglarını kaydettiniz ve nihai cevapları çıkardınız. Şimdi, bu logları ve sonuçları çeşitli kalitatif ve kantitatif yaklaşımlar kullanarak analiz etmemiz, grafikler ve tablolar oluşturmamız ve bulgularımızı yayına hazırlamamız gerekiyor.

### Temel Araştırma Sorusu

Şu anda, yapay zeka kod asistanı pazarı kod tabanını (codebase) anlama konusunda iki baskın yaklaşıma bölünmüş durumdadır:

1. **Semantic Search (RAG):** Modern AI IDE'leri (Cursor, GitHub Copilot gibi) araçlar kod tabanınızı önceden bir vektör veritabanına indeksler. Bu sayede agent'ların ilgili kod parçalarını semantic search yoluyla anında bulmak için Retrieval-Augmented Generation (RAG) kullanmasına olanak tanırlar.
2. **Agentic Search:** Terminalde yaşayan bağımsız kod agent'ları (Claude Code, Gemini CLI, OpenHands, Mistral Vibe ve DeepAgents gibi) RAG **kullanmazlar** ve kod tabanını önceden indekslemezler. Bunun yerine, tamamen "Agentic Search" adı verilen yönteme dayanırlar; çalışma alanında gezinmek için aktif olarak komutlar çalıştırır (`grep`, `find`, `ls` gibi) ve dosyaları dinamik olarak okurlar.

**Temel araştırma sorumuz birbiriyle yarışan bu iki yaklaşımı titizlikle karşılaştırmaktır.**

Her bir agent için araç setlerini kesin bir şekilde kısıtlamamızın nedeni tam olarak budur. ReAct Agent, RAG/Semantic Search yaklaşımını temsil ederken, Deep Agent saf Agentic Search yaklaşımını temsil etmektedir.

### Beklenen Sonuçlar Üzerine Önemli Bir Not

Önceden belirlenmiş "Deep Agent'lar daha iyidir" veya "ReAct daha iyidir" gibi bir önyargımız **yoktur.** Dahası, bu projede onların temel algoritmik yapılarını iyileştirmeye de çalışmıyoruz. Hedefimiz kesinlikle her iki mimariyi **analiz etmek, karşılaştırmak ve artılarını ile eksilerini keşfetmektir.**

Eğer deneyleriniz Deep Agent'ların çok daha fazla token harcamasına rağmen daha kötü sonuçlar aldığını gösteriyorsa, **bu tamamen sorunsuzdur ve harika bir bulgudur!** Aslında, Deep Agent'lar için çıkacak negatif bir sonuç, makalemizi zayıflatmak yerine daha da güçlendirecektir. Bu durum, piyasada basit RAG yerine karmaşık agentic search'ü fazlasıyla öven mevcut endüstri trendine karşı veriye dayalı taze bir bakış açısı ve güçlü bir karşıt argüman sunar.

---

## 2. Değerlendirme Yönergeleri

*Artık deneyleriniz bittiğine göre, verileri değerlendirmek için aşağıdaki yönergeleri izleyin:*

## 2. Zorunlu Analizler (Temel Metrikler)

Her grup aşağıdaki iki temel analizi mutlaka tamamlamalıdır. Bunlar araştırma makalenizin kantitatif temelini oluşturacaktır.

### A. Doğruluk (Accuracy) Değerlendirmesi (SWE-QA Rubric)

Agent'larınızın ürettiği nihai cevapları, SWE-QA veri setinin sağladığı resmi puanlama kriterlerini (rubric) kullanarak değerlendirmelisiniz.

- Cevapları, doğru bilgiyi başarılı bir şekilde bulup bulmadıklarına ve bu bilgiyi doğru bir şekilde sentezleyip sentezlemediklerine göre notlandıracaksınız.
- **Çıktı:** Hem ReAct Agent (RAG) hem de Deep Agent (Agentic Search) için Başarılı (Pass) / Başarısız (Fail) / Kısmi Başarı (Partial Success) oranlarını gösteren net bir karşılaştırma tablosu.

### B. Maliyet ve Verimlilik Analizi

Yazılım mühendisliğinde sadece doğruluk (accuracy) yeterli değildir; o doğruluğa ulaşmanın maliyetini de ölçmeliyiz. Benchmarking sırasında kaydettiğiniz trace loglarını kullanarak, her iki mimari için aşağıdakileri hesaplayın ve grafikleştirin:

- **Toplam Araç Kullanımı (Total Tool Calls):** Soru başına gereken ortalama araç çağrısı sayısı.
- **Token Tüketimi:** Soru başına harcanan ortalama girdi (input) ve çıktı (output) token sayısı.
- **Finansal Maliyet:** Token kullanımını, seçtiğiniz LLM'in fiyatlandırma tarifesine göre dolar bazında maliyete çevirin.
- **Pareto Frontier (Kritik):** (ArtificialAnalysis.ai'da bulunan endüstri benchmark'larına benzer) bir "Doğruluk vs. Maliyet" (Accuracy vs. Price) grafiği oluşturun. Bu görsel, Deep Agent'ın sunabileceği olası doğruluk artışının, harcadığı devasa token artışına değip değmediğini anında gösterecektir.

---

## 3. Keşifsel Analiz (Serbest Seçim)

Makalenizi benzersiz kılmak ve derin içgörüler ortaya çıkarmak için, **her öğrenci grubu kendi seçeceği ekstra 2 veya 3 farklı analiz türünü daha yapmalıdır.** Kendi analiz yöntemlerinizi tasarlamakta tamamen özgürsünüz.

Tüm ham execution loglarını eksiksiz kaydettiğiniz için, yapay zekanın nasıl "düşündüğü" ve arama yaptığı konusunda elinizde bir veri madeni var. Aşağıda seçebileceğiniz veya ilham alabileceğiniz makaleye çok uygun bazı fikirlerin bulunduğu bir "menü" yer almaktadır:

#### Fikir 1: "Ormanda Kaybolma" Analizi (Trajectory Length)

Daha fazla adım atan (daha çok tool call yapan) agent'lar gerçekten cevaba daha mı çok yaklaşıyor, yoksa sadece halüsinasyon döngülerine mi sıkışıyor?

- **Yöntem:** Tool call sayısını Başarı/Başarısızlık (Pass/Fail) oranına karşı grafikleştirin. Deep Agent'ın ilk 5 tool call içinde cevabı bulamadığı durumlarda, bağlam penceresi (context window) kirlendiği için başarı şansının %0'a yaklaştığını keşfedebilirsiniz.

#### Fikir 2: Error Taxonomy (Hata Sınıflandırması)

Bir agent başarısız olduğunda *tam olarak neden* başarısız oldu?

- **Yöntem:** Başarısız olan sorulardan bir örneklem alın ve logları manuel olarak kategorize edin.
  - *Retrieval Failure (Arama Hatası):* `grep` kullandı ama yanlış anahtar kelimeyi aradı.
  - *Context Poisoning (Bağlam Kirlenmesi):* Doğru dosyayı okudu ama yanında 10 tane de alakasız dosya okuyup LLM'in kafasını karıştırdı.
  - *Synthesis Failure (Sentez Hatası):* Kodun tam olarak doğru satırlarını buldu, ancak LLM mantığı kurup doğru cevabı çıkaramadı.

#### Fikir 3: "Gürültüye Karşı Sinyal" Oranı (Context Efficiency)

Hangi mimari okuduğu şeyler konusunda daha "temiz"?

- **Yöntem:** Semantic Search (RAG) sadece belirli kod parçalarını (chunks) getirirken, Agentic Search genelde tüm dosyaları veya devasa `grep` çıktılarını okur. Süreç boyunca "Faydalı Tokenların" (cevabı barındıran asıl kod satırları) "Okunan Toplam Tokenlara" oranını hesaplayın. Bu oran Agentic Search'ün içeri çok fazla "çöp" (garbage) bağlam taşıyıp taşımadığını kanıtlar.

#### Fikir 4: "Kulaktan Kulağa" Etkisi (Sadece Deep Agent)

Deep Agent'lar sub-agent'lar ve bir planner (planlayıcı) kullandığına göre, mesajlar ileri geri aktarılırken bilgi kayboluyor mu?

- **Yöntem:** *Sub-Agent*'ın dosya sisteminde cevabı başarıyla bulduğu, ancak bulgularını *Main Orchestrator Agent*'a özetlerken Orchestrator'ın bunu yanlış anladığı veya kritik detayları atladığı örnekleri bulmak için logları izleyin.

#### Fikir 5: Araç Kullanım Isı Haritası (Tool Usage Heatmap)

Sorunları gerçekten hangi araçlar çözüyor?

- **Yöntem:** Araç kullanım sıklığının bir dökümünü çıkarın. Deep Agent gerçekten karmaşık planlama araçlarını kullanıyor mu, yoksa zamanının %90'ında sadece `grep` mi spamlıyor? Bu, karmaşık araç alanlarının modeller tarafından gerçekten verimli kullanılıp kullanılmadığını kanıtlayacaktır.


**NOT:** Makaleyi güçlendireceğini düşündüğünüz her türlü grafik/tablo/görselleştirme/analiz türünü kullanmakta özgürsünüz.
