# 2. Hafta: Scaffolding

## Genel Bakış

Bu hafta kod yazmaya başlamalısınız. Bu projede sadece vibe-coding yapmalısınız; yani kendi başınıza kod yazmamalı, AI Agent kullanarak prompt engineering yoluyla kod üretmelisiniz. Öğrenci e-postanızla ücretsiz kullanabileceğiniz iki araç Google Antigravity ve Github Copilot (VSCode extension) şeklindedir.

Kısaca özetlemek gerekirse, bu projede iki farklı mimariye (ReAct ve Deep Agents) sahip farklı code agents implementasyonu yapacak, bunların SWE-QA dataset üzerindeki performanslarını karşılaştıracak ve sonuçları bir research paper'da sunacaksınız. Ayrıca, kullanıcıların herhangi bir codebase hakkında soru sorabilmesi için bir chatbot UI oluşturacaksınız.

## Ön Koşullar

#### MCP ile Vibe-Coding Araçları
Vibe-coding araçlarınızın hazır olduğundan emin olun. Seçtiğiniz her araç MUTLAKA DeepWiki MCP ve LangChain MCP server'larına bağlı olmalıdır. Bu araçlar, AI agents'ın güncel LangChain/Deep-Agents documentation bilgilerini gerçek zamanlı olarak sorgulamasını ve sizin için doğru kodları yazmasını sağlar. Promptlarınızda DeepWiki MCP ve LangChain MCP server'larını kullanmasını istemeyi ASLA unutmayın. Yoksa AI agent'lar eski documentation bilgilerini kullanarak size yanlış kodlar yazabilir!

Vibe-coding aracınızdaki LLM için istediğiniz modeli seçebilirsiniz, ancak hem yetenekli hem de cost-effective olmaları nedeniyle "Gemini Flash 3.0" ve "GPT 5.4 mini" kullanmanız önerilir. Aksi takdirde aylık krediniz hızla tükenebilir.

#### API Key
Bildiğiniz gibi, implemente edeceğiniz bu AI Agents beyin olarak LLMs kullanmaktadır. Bu proje için gereken LLMs için büyük GPU'lar gereklidir ve bizde bu imkanlar bulunmamaktadır. Bu nedenle agent'ınızı bulut LLMs platformlarına bağlamalısınız.

LLM Inference'ı ücretsiz edinmek için birkaç seçeneğiniz bulunmaktadır:

- [Google AI Studio](https://aistudio.google.com/) : Google'ın LLMs modellerini kullanabileceğiniz bir platformdur. Burada günlük limitleri olan bir API Key alabilirsiniz. En yüksek limitlere sahip olan "Gemini Lite" serisi gibi en ucuz modelleri kullanmanızı öneririm. Birden fazla e-posta ile hesap açarak birden fazla key edinebilirsiniz.

- [OpenRouter](https://openrouter.ai/) : Dünyadaki neredeyse tüm cloud LLMs modellerine erişim sağlayan bir platformdur. Bazı modelleri sınırlı günlük kota ile ücretsizdir. Birden fazla e-posta ile hesap açarak birden fazla key edinebilirsiniz.

- [Google Cloud](https://cloud.google.com/pricing?hl=en) : Google Cloud yaklaşık 300$ tutarında ücretsiz kredi sağlar ve bunu LLMs çalıştırmak için kullanabilirsiniz. Bu krediyi şu an kullanmamanızı, SWE-QA dataset üzerindeki research paper deneyleriniz için saklamanızı öneririm. Bunun için Google'ın [Vertex AI](https://cloud.google.com/vertex-ai?hl=en) servisini kullanmalısınız.

- [Azure](https://azure.microsoft.com/en-us/products/ai-services/openai-service) : Azure, github student pack (üniversite e-postanızla alabileceğiniz) ile yaklaşık 100$ tutarında ücretsiz kredi sağlamaktadır. Bu krediyi şu an kullanmamanızı, SWE-QA dataset üzerindeki research paper deneyleriniz için saklamanızı öneririm. Bunun için [Azure Foundry](https://azure.microsoft.com/en-us/products/ai-foundry/models) servisini kullanmalısınız.

## Görevler

Bu hafta sadece bir Deep Agent ve bunun UI kısmını implemente edeceksiniz.

#### 1. UI Kurulumu
Bu proje için ilerleyen zamanlarda bir UI yazacaksınız. Ancak şu an ilerlemek ve daha hızlı prototype oluşturmak için LangChain tarafından sağlanan UI'ı kullanabilirsiniz:
- [Deep Agents UI](https://github.com/langchain-ai/deep-agents-ui)

#### 2. Deep Agent Implementasyonu
Yazılım repository'si hakkındaki soruları cevaplayabilen bir Deep Agent implementasyonu yapmak için Langchain Deep Agents library (Python versiyonu) kullanın.
- [Langchain Deep Agents](https://github.com/langchain-ai/deepagents)

Bu Deep Agent, Deep Agent library içindeki tüm varsayılan araçlara sahip olmalıdır:
- Planning Tool
- Virtual Filesystem
- Shell 
- Sub-agents
- Context Summarization

ÖNEMLİ NOT: Deep Agent implementasyonu yaparken vibe-coding aracınızdan "pip" yerine "uv" package manager kullanmasını isteyin. Çünkü "uv", "pip"e göre çok daha hızlı ve verimlidir.

#### 3. Agent ve UI Bağlantısı
Agent'ı, UI'ın documentation ve README kısmında gösterildiği gibi `langgraph dev` kullanarak deploy edin.

#### 4. Agent'a Soru Sormak
Agent'a istediğiniz bir code repository'si için erişim verin ve ondan repo hakkında soruları cevaplamasını isteyin. Örneğin, "Explain the architecture of this repository" veya "Find the function that handles user authentication" gibi sorular sorabilirsiniz.

#### 5. Kodlarınızı Paylaşın
Bu proje için bir frontend ve bir backend repository'miz olacak. Şimdilik frontend için LangChain'in sağladığı UI'ı kullanın ve kendi github hesabınızda bunun için bir github repository oluşturun. Ayrıca backend için de kendi github hesabınızda başka bir repository oluşturun.

Tüm kodlarınız her zaman kendi github hesabınızda olmalı ve kodunuzun güncel versiyonunu düzenli olarak commit ve push yapmalısınız. Git'i etkili bir şekilde kullanmalı ve küçük değişiklikler için bile sık sık commit ve push yapmalısınız.

Eğer vibe-coding araçlarınıza Github MCP server eklerseniz, vibe-coding aracınız git operasyonlarını sizin yerinize yönetebilir.

Bu repository'lerin linklerini benimle paylaşın ve beni collaborator olarak ekleyin.
Github adresim: https://github.com/amirkiarafiei
E-postam: amirkia.rafiei@gmail.com
