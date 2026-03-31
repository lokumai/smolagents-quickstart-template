# 3. Hafta: Agent Uygulaması ve UI Entegrasyonu

## Genel Bakış

Bu hafta, geçen hafta başladığınız Deep Agent kurulumunun üzerine, baseline agent mimarisini kuracaksınız ve her iki agent'ı da tek bir kullanıcı arayüzünde (UI) birleştireceksiniz.

Her zamanki gibi "Vibe-Coding" araçlarınızı kullanın. AI asistanlarınızın güncel kod yazabilmesi için LangChain Docs ve DeepWiki MCP server bağlantılarının aktif olduğundan emin olun.

## Görevler

### 1. Baseline Agent'ı Kurun

İlk büyük göreviniz, LangChain kütüphanesinin en güncel versiyonunu kullanarak standart bir agent mimarisi kurmaktır. Bu agent, Deep Agent ile karşılaştırma yapmak için bizim temel (baseline) modelimiz olacak.

**Önemli LangChain Güncellemesi:** LangChain'in son versiyonlarında "ReAct Agent" terimi artık kullanılmıyor. Bunun yerine sadece "Agent" deniliyor ve bu agent `create_agent()` metodu ile oluşturuluyor. Biz yine de buna konsept olarak baseline veya "ReAct-style" agent diyeceğiz.

- **Action Space (Araçlar):** Bu agent sadece SWE-QA paper'ında tanımlanan araçlarla sınırlandırılmalıdır. Agent'a **sadece** şu üç aracı vermelisiniz:
  1. `read_file`
  2. `get_repo_structure`
  3. `search_rag`
- **Kısıtlama:** Bu agent'a başka hiçbir extra araç (shell access, planning, filesystem writing gibi) vermeyin. Agent sadece bu üç aracı kullanarak kod tabanında gezerek cevap bulmalıdır.

### 2. UI Güncelleme ve Özelleştirme

Backend tarafında hem Deep Agent hem de bu hafta kurduğunuz standart Agent hazır olduktan sonra, bunları frontend tarafında birleştirmeniz gerekiyor.

- **GUI Özelleştirme:** Fork ettiğiniz Deep-Agents UI projesinde değişiklik yapın.
- **Setup Selector:** Kullanıcının görebileceği bir dropdown menü veya toggle ekleyin. Kullanıcı bir soru sormadan önce hangi mimariyi kullanmak istediğini seçebilmeli:
  - Agent (Standard/ReAct)
  - Deep Agent

### 3. Test ve Deployment

Entegrasyon bittikten sonra uçtan uca test yapın:

- Backend'e örnek bir repository verin.
- UI üzerinden Standard Agent'ı seçip zor bir mimari soru sorun. Agent'ın kendi araçlarını nasıl kullandığını izleyin.
- Sonra Deep Agent'ı seçip aynı soruyu sorun. Planlama ve sub-agent aşamalarını karşılaştırın.

## Başarı Kriterleri

Gelecek haftaki toplantıda şunları göstermelisiniz:

1. Kullanıcının Agent veya Deep Agent seçebildiği çalışan bir chatbot UI.
2. Seçilen agent mimarisi ile bir kod tabanı hakkında soru sorup cevap alabilme.
3. Hem frontend hem de backend kodlarının GitHub repository'lerinize push edilmiş olması.

---

## Teknik Rehber: İki agent'ı aynı UI'a nasıl bağlarız?

Hem Standard Agent'ı hem de Deep Agent'ı aynı UI içinde çalıştırmak için **LangGraph Graph ID** yapısını kullanacağız.

Her iki mimari de aynı LangChain-native altyapıyı kullandığı için Deep Agent UI her ikisini de destekleyebilir. İki ayrı backend kurmanıza gerek yok. Bunun yerine:

### 1. Unified Backend Mimarisi

İki agent kodunu da aynı repository'de tutun. `langgraph dev` komutunu çalıştırdığınızda, her iki agent da aynı port üzerinden (örn: `127.0.0.1:2024`) erişilebilir olacaktır.

`langgraph.json` dosyanızda ikisini de tanımlayın:

```json
{
  "graphs": {
    "standard_agent": "./baseline_agent.py:graph",
    "deep_agent": "./deep_agent.py:graph"
  },
  "env": ".env"
}
```

### 2. State Schema Uyumu (UI için Kritik)

Her iki agent da konuşma geçmişini mutlaka `messages` adlı bir key'de tutmalıdır. UI'daki `ChatInterface` bileşeni bu key'i dinler.

### 3. Frontend Entegrasyonu (Deep-Agents UI)

Frontend, backend ile konuşmak için `@langchain/langgraph-sdk` kullanır. Selector eklemek için:

- **Kullanılacak Hook**: UI içindeki `useChat` hook'u bir `assistantId` parametresi alır.
- **Selector**: `activeAgentId` state'ini güncelleyen basit bir React bileşeni (dropdown) oluşturun.
- **Dinamik Bağlantı**: Bu `activeAgentId` değerini LangGraph client konfigürasyonuna geçirin. Kullanıcı seçimi değiştirdiğinde UI ilgili graph ID'ye (`standard_agent` veya `deep_agent`) bağlanacaktır.

> [!TIP]
> **AI Aracınıza sormak için prompt örneği:**
> *"I have two LangGraph graphs defined in my backend: 'standard_agent' and 'deep_agent'. Update the Deep-Agents UI (Next.js) to include a dropdown selector that allows the user to switch the `assistantId` used by the `useChat` hook so they can toggle between these two agents at the start of a thread."*
