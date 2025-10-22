# 🧠 Neuroscience Chatbot: Zihninizin Potansiyelini Keşfedin

**Akbank GenAI Bootcamp: Yeni Nesil Proje Kampı Final Projesi**

Bu proje, RAG (Retrieval Augmented Generation) mimarisine dayalı, nörobilimsel konular hakkında soruları yanıtlayan, hafızalı ve çok dilli bir chatbot'tur. Proje, modern ve interaktif bir web arayüzü üzerinden sunulmaktadır.

---

## 🚀 Canlı Demo & Arayüz

Nörobilim Asistanı'nı canlı olarak test etmek için aşağıdaki linke tıklayabilirsiniz. Arayüz, alışkanlıklar, motivasyon, erteleme ve beynin çalışma prensipleri gibi konularda hem Türkçe hem de İngilizce soruları yanıtlayabilir.

**👉 [https://bb718df71b4bb1b43e.gradio.live/]**

*(`Önemli Not:` Bu link, Gradio tarafından oluşturulmuş geçici bir tüneldir ve 72 saat sonra sona erebilir. Linkin çalışması için projenin Colab not defterinin arka planda aktif olması gerekmektedir. Eğer link çalışmıyorsa, projenin canlı demosu için iletişime geçebilirsiniz.)*

### Arayüz Görüntüleri

| Ana Arayüz & Türkçe Soru | İngilizce Soru & Cevap |
| :---: | :---: |
| ![Ana Arayüz](https://github.com/Fatmanurkntr/Neuroscience-Chatbot/blob/main/chatbotekran.png?raw=true) | ![Hafıza Testi](https://github.com/Fatmanurkntr/Neuroscience-Chatbot/blob/main/chatbotekran1.png?raw=true) |

| Türkçe Soru & Cevap | Hafıza Takipli Soru |
| :---: | :---: |
| ![İngilizce Test](https://github.com/Fatmanurkntr/Neuroscience-Chatbot/blob/main/chatbotekran2.png?raw=true) | ![Bilimsel Soru](https://github.com/Fatmanurkntr/Neuroscience-Chatbot/blob/main/chatbotekran3.png?raw=true) |

### Product Kılavuzu
Arayüzde sizi basit ve kullanıcı dostu bir sohbet ekranı karşılayacaktır.
1. Metin kutusuna sorunuzu yazın ve "Enter"a basın.
2. Chatbot, sorunuzun dilini algılayacak ve o dilde cevap üretecektir.
3. Önceki sorularınızı hatırlayarak, sohbetin devamını getirebilirsiniz. (Örn: "Erteleme nedir?" dedikten sonra "Peki bununla nasıl başa çıkabilirim?" diye sorabilirsiniz.)
4. "Denemek için bir soru seçin:" bölümündeki örneklere tıklayarak chatbot'u hızlıca test edebilirsiniz.

---

## 🎯 Projenin Amacı ve Çözdüğü Problem

**Problem:** İnsanlar, alışkanlıklarını değiştirme, motivasyonlarını artırma veya erteleme gibi davranışsal zorluklarla karşılaştıklarında, bu durumların arkasındaki bilimsel gerçeklere genellikle karmaşık ve akademik bir dille ulaşırlar. Bu bilgileri anlamak ve günlük hayata uygulamak zordur.

**Amaç:** Bu projeyle, karmaşık nörobilimsel bilgileri, herkesin anlayabileceği, pratik ve eyleme geçirilebilir tavsiyelere dönüştüren bir "koç" kimliğinde yapay zeka asistanı geliştirmek hedeflenmiştir. Chatbot, bilimsel bir temele dayanarak güvenilir cevaplar sunarken, kullanıcıyla empatik ve destekleyici bir diyalog kurar.

---

## 📚 Veri Seti

Projenin bilgi bankası olarak Hugging Face platformunda yer alan `sydonayrex/fineweb-edu-neuroscience` veri seti kullanılmıştır.

- **İçerik:** Bu veri seti, yüksek kaliteli **Fineweb-EDU** koleksiyonundan, `"neuroscience"` ve `"educational psychology"` anahtar kelimeleriyle filtrelenerek oluşturulmuştur. Veri seti, toplam **25,944 satırdan** oluşmakta ve her bir satır, zengin bir İngilizce metin parçası (extract) içermektedir.
- **Seçim Nedeni:** Akademik makaleler, blog yazıları ve eğitim materyallerinden oluşan bu çeşitli içerik, projenin konusu olan motivasyon, alışkanlıklar ve beyin fonksiyonları hakkında derinlemesine ve güvenilir bir bilgi temeli sunmaktadır.
- **Hazırlık Metodolojisi:** Veri setindeki bu 25,944 metin parçası, LangChain'in `RecursiveCharacterTextSplitter` aracı kullanılarak, RAG mimarisinin verimli bir şekilde işleyebileceği yaklaşık **300,000 adet** daha küçük ve anlamlı alt parçaya (chunk) bölünmüştür.

---

## 🛠️ Çözüm Mimarisi ve Kullanılan Teknolojiler

Proje, Büyük Dil Modelleri'nin (LLM) halüsinasyon riskini ortadan kaldırmak ve cevapları doğrulanabilir bir bilgi kaynağına dayandırmak amacıyla **RAG (Retrieval Augmented Generation)** mimarisi üzerine kurulmuştur.

**Çalışma Akışı:**
1. Kullanıcının sorusu alınır ve dili tespit edilir.
2. Soru, arama yapılabilmesi için İngilizce'ye çevrilir.
3. `all-mpnet-base-v2` modeli ile soru bir vektöre dönüştürülür.
4. `ChromaDB` vektör veritabanında bu soruyla anlamsal olarak en alakalı metin parçaları bulunur.
5. Bulunan metinler, sohbet geçmişi ve kullanıcının orijinal sorusu, `Gemini` modeline özel bir prompt şablonu ile gönderilir.
6. `Gemini`, bu bağlama dayanarak, kullanıcının sorduğu dilde ve "koç" kimliğinde bir cevap üretir.

**Teknoloji Yığını:**
- **Uygulama Çatısı:** LangChain
- **Dil Modeli (LLM):** Google Gemini 2.5 Flash
- **Embedding Modeli:** `sentence-transformers/all-mpnet-base-v2` (Hugging Face)
- **Vektör Veritabanı:** ChromaDB
- **Web Arayüzü:** Gradio

---

## ⚙️ Kodun Çalışma Kılavuzu

Bu projenin kodlarını kendi ortamınızda (örneğin Google Colab) çalıştırmak için aşağıdaki adımları izleyebilirsiniz.

### 1. Proje Dosyalarını Edinme (Klonlama)

Öncelikle, projenin tüm dosyalarını içeren bu GitHub reposunu komut satırı aracılığıyla kendi bilgisayarınıza veya bulut ortamınıza klonlayın:

```bash
git clone https://github.com/Fatmanurkntr/Neuroscience-Chatbot.git
cd Neuroscience-Chatbot
```

### 2. Gerekli Kütüphaneleri Kurma
Projenin çalışması için gereken tüm kütüphaneler `requirements.txt` dosyasında listelenmiştir. Bu kütüphaneleri aşağıdaki komutla tek seferde kurabilirsiniz:
```bash
pip install -r requirements.txt
```

### 3. API Anahtarını Ayarlama
Proje, Google Gemini API'sini kullanmaktadır. Bir Google API anahtarı almanız ve bunu not defterinin çalıştığı ortamda (örneğin Colab Secrets) `GOOGLE_API_KEY` adıyla kaydetmeniz gerekmektedir.

### 4. Projeyi Çalıştırma
- `Neuroscience_Chatbot_FINAL.ipynb` not defterini bir Jupyter ortamında (Google Colab, VS Code vb.) açın.
- Not defterindeki Markdown açıklamalarını takip ederek hücreleri sırayla çalıştırın.
- **Önemli Not:** Bölüm 1'deki kütüphane kurulumundan sonra, not defteri oturumunu yeniden başlatmanız (`Runtime -> Restart session`) gerekmektedir.
- **Kritik Uyarı:** **Bölüm 2 (Bilgi Bankasının İnşası)**'yi çalıştırmanıza gerek yoktur. Proje, daha önce oluşturulmuş ve Google Drive'da saklanan hazır veritabanını kullanacak şekilde tasarlanmıştır.

---

## 📊 Elde Edilen Sonuçlar ve Geliştirme Süreci

Bu bölümde, projenin ulaştığı nihai yetenekler ve bu süreçte karşılaşılan zorluklardan çıkarılan dersler özetlenmektedir.

-   🚀 **Başarı:** Proje sonucunda, hedeflenen tüm temel ve ileri düzey yeteneklere sahip bir chatbot başarıyla geliştirilmiştir. Bu yetenekler şunlardır:
    -   **Güvenilir Bilgi:** RAG mimarisi sayesinde, cevaplar bilimsel bir veri setine dayandırılmış ve halüsinasyon riski ortadan kaldırılmıştır.
    -   **Konuşma Hafızası:** Chatbot, önceki konuşmaları hatırlayarak daha akıcı ve bağlama uygun diyaloglar kurabilmektedir.
    -   **Çok Dillilik:** Arka planda çalışan dil tespiti ve çeviri katmanı sayesinde, kullanıcılar sorularını kendi dillerinde sorabilmekte ve yine kendi dillerinde cevap alabilmektedir.
    -   **Web Arayüzü:** Gradio ile geliştirilen modern ve kullanıcı dostu arayüz, projenin herkes tarafından kolayca test edilmesini sağlamaktadır.

-   🛠️ **Zorluklar ve Öğrenilenler:** Geliştirme sürecinde, modern yapay zeka projelerinin doğası gereği birçok teknik zorlukla karşılaşılmış ve bu zorluklar metodik bir hata ayıklama süreciyle aşılmıştır:
    -   **Bağımlılık Yönetimi (`Dependency Hell`):** Projenin en büyük zorluğu, `langchain`, `google-generativeai` ve `chromadb` gibi hızla gelişen kütüphaneler arasındaki versiyon uyumsuzlukları olmuştur. Bu durum, `ModuleNotFoundError` ve `ResolutionImpossible` gibi kritik kurulum hatalarına yol açmıştır.
        -   **Öğrenilen Ders:** Kütüphaneleri `pip install -U library` gibi basit komutlarla kurmak yerine, `langchain[google-genai]` gibi entegrasyonu garantileyen özel kurulum komutları kullanmanın veya kütüphaneleri mantıksal gruplar halinde kurmanın bu tür çakışmaları önlediği öğrenilmiştir.
    -   **Colab Ortamının İncelikleri:** Google Colab'de, `pip install` ile yeni bir kütüphane kurulduktan sonra, çalışan oturumun (kernel) bu yeni kütüphaneyi otomatik olarak tanımadığı tespit edilmiştir.
        -   **Öğrenilen Ders:** Kurulum işlemlerinden sonra Colab oturumunu manuel olarak yeniden başlatmanın (`Runtime -> Restart session`) "Altın Kural" olduğu ve bu adımın `import` hatalarını kesin olarak çözdüğü anlaşılmıştır.
    -   **API ve Model Erişimi:** Proje sırasında kullanılan `gemini-1.5-flash` gibi "ön izleme" (preview) modellerine erişimin, API anahtarının yetkilerine ve Google'ın anlık güncellemelerine bağlı olarak değişkenlik gösterebildiği görülmüştür.
        -   **Öğrenilen Ders:** Bir modelin `Not Found (404)` hatası vermesi durumunda, kütüphaneyi suçlamadan önce `genai.list_models()` gibi yöntemlerle o anki hesap için mevcut olan modelleri doğrulamanın ve kodda bu güncel model adını kullanmanın önemi kavranmıştır.
    -   **Bu süreç, bir yapay zeka projesinin başarısının sadece iyi bir kod yazmaktan değil, aynı zamanda sağlam bir ortam kurma, sabırlı hata ayıklama ve kullanılan araçların iç dinamiklerini anlama becerisinden geçtiğini göstermiştir.**
