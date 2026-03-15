# 1. Hafta: Ön Koşullar ve Geliştirme Ortamı Kurulumu

Bu projede, bir yazılım reposunun mimarisi ve mantığı hakkındaki karmaşık soruları yanıtlayan bir AI Agent chatbot tasarlayacağız. İki farklı agent mimarisi kullanacağız: ReAct Agent ve Deep Agent. Son olarak, bu iki agent'ın SWE-QA dataset üzerindeki performansını ve verimliliğini karşılaştıran bir akademik makale yazıp yayınlayacağız.

Aşağıda ilk hafta için ön koşullar ve yapılması gereken görevler listelenmiştir.

---

## Bölüm 1: Teorik Temeller (Öğrenilecekler)
Modern AI mimarilerinin kelime dağarcığını ve temel çalışma mantığını anlamalısınız. Lütfen aşağıdaki kavramları araştırıp okuyun:

- [ ] **LLM Temelleri:** Large Language Model nedir? Context window, token, temperature ve API limitlerini anlayın.
- [ ] **RAG (Retrieval-Augmented Generation):** Yanıt vermeden önce Vector Database kullanarak ilgili metin parçalarını geri getirip bir LLM'e "hafıza" kazandırma yöntemini öğrenin.
- [ ] **Tool Calling:** LLM'lerin dış dünyayla (örn. hava durumunu getirme, dosya okuma) nasıl etkileşime geçtiğini öğrenin.
- [ ] **MCP (Model Context Protocol):** Nedir? Neden AI sistemlerini harici verilere bağlamak için yeni standarttır?
- [ ] **MCP Servers:** MCP Servers'ın nasıl çalıştığını ve özel verileri veya araçları bir LLM için nasıl erişilebilir kıldığını anlayın.
- [ ] **LLM vs. Agent:** Basit bir metin üretim modeli ile otonomisi ve hedefleri olan bir "Agent" arasındaki fark nedir?
- [ ] **ReAct Agent (Multi-step Agent):** "Reason-then-Act" döngüsünü öğrenin. Bir agent çevresini nasıl sürekli gözlemler ve bir hedefe ulaşana kadar nasıl döngüde kalır?
- [ ] **Deep Agent:** [LangChain Deep Agents Documentation](https://docs.langchain.com/oss/python/deepagents/overview) sayfasına başvurun. Hiyerarşik mimarilerin, task decomposition (planlama) ve sub-agents kullanımının standart ReAct agent'larda bulunan context overflow sorunlarını nasıl çözdüğünü anlayın.

---

## Bölüm 2: Ortam Kurulumu (Yapılacaklar)
Bir AI araştırmacısı olarak kullandığınız araçlar kusursuz olmalıdır. "Vibe-Coding" ortamınızı kurmak için aşağıdaki adımları izleyin. Bu projede kod yazmanıza izin verilmemektedir; ancak, Copilot ve Antigravity gibi araçlardaki Code Agents'a prompt vererek kodları sizin yerinize yazmalarını sağlamalısınız.

### 1. Version Control Kurulumu
- [ ] **Git & GitHub Öğrenin:** Git bilmiyorsanız hızlı bir eğitime katılın (crash course). Commit, push, pull ve branch yapmayı bilmelisiniz.
- [ ] **Repository Setup:** Ana proje repository'sine erişiminiz olduğundan ve projeyi lokal bilgisayarınıza clone'layabildiğinizden emin olun.

### 2. Antigravity (Gemini Pro) Kurulumu
- [ ] **Aboneliğinizi Edinin:** Gemini Pro Student aboneliğine kayıt olun.
- [ ] **Antigravity Kurulumu:** Antigravity uygulamasını makinenize kurun.
- [ ] **MCP Servers Bağlantısı:** Yapay zeka asistanınızın bir alan uzmanı (domain expert) olabilmesi için Antigravity kurulumunuzu aşağıdaki MCP Servers'a bağlayın:
    - **LangChain Docs MCP** (güncel kütüphane sözdizimini bilmesi için)
    - **DeepWiki MCP** (repository analizi pattern'lerini bilmesi için)

### 3. VS Code & Copilot Pro Kurulumu
- [ ] **GitHub Student Developer Pack Edinin:** Üniversite e-postanızı kullanarak student pack'e başvurun.
- [ ] **Copilot Pro'yu Aktif Edin:** Student Dev Pack üzerinden ücretsiz Copilot Pro aboneliğinizi başlatın.
- [ ] **VS Code Eklentisini Kurun:** Visual Studio Code içerisine GitHub Copilot eklentisini kurun.
- [ ] **Copilot'a MCP Servers Bağlantısı:** VS Code/Copilot'u da **LangChain Docs** ve **DeepWiki** MCP servers'a bağlanacak şekilde yapılandırın, böylece editör içi kod tamamlamalarınız (completions) context-aware olacaktır.

---
> [!TIP]
> **Neden bu kadar kurulum yapıyoruz?** 
> 2. Hafta başladığında tamamen *fikirlere, workflow'a ve deneylere* odaklanmanızı istiyoruz. Bir bug ile karşılaştığınızda, IDE'niz LangChain dökümanlarını okuyup sizin yerinize bunu düzeltecek kadar akıllı olmalıdır.
