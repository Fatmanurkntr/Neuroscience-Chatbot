# 🧠 Neuroscience Chatbot: Zihninizin Potansiyelini Keşfedin

**Akbank GenAI Bootcamp: Yeni Nesil Proje Kampı Final Projesi**

Bu proje, RAG (Retrieval Augmented Generation) mimarisine dayalı, nörobilimsel konular hakkında soruları yanıtlayan, hafızalı ve çok dilli bir chatbot'tur. Proje, bir web arayüzü üzerinden sunulmaktadır.

---

## 🚀 Canlı Demo & Arayüz

Nörobilim Asistanı'nı canlı olarak test etmek için aşağıdaki linke tıklayabilirsiniz. Arayüz, alışkanlıklar, motivasyon, erteleme ve beynin çalışma prensipleri gibi konularda hem Türkçe hem de İngilizce soruları yanıtlayabilir.

**👉 [CANLI DEMO LİNKİNİ BURAYA YAPIŞTIR]**

*(Not: Bu link, Gradio tarafından oluşturulmuş geçici bir tüneldir ve 72 saat sonra sona erebilir. Linkin çalışması için projenin Colab ortamında aktif olması gerekmektedir.)*

### Arayüz Görüntüsü
![Nörobilim Asistanı Arayüzü]([ARAYÜZÜN EKRAN GÖRÜNTÜSÜNÜN GITHUB LİNKİNİ BURAYA YAPIŞTIR])
*(İpucu: Ekran görüntüsünü reponuza yükleyin ve resmin linkini buraya ekleyin.)*

### Product Kılavuzu
Arayüzde sizi basit ve kullanıcı dostu bir sohbet ekranı karşılayacaktır.
1.  Metin kutusuna sorunuzu yazın ve "Enter"a basın.
2.  Chatbot, sorunuzun dilini algılayacak ve o dilde cevap üretecektir.
3.  Önceki sorularınızı hatırlayarak, sohbetin devamını getirebilirsiniz. (Örn: "Erteleme nedir?" dedikten sonra "Peki bununla nasıl başa çıkabilirim?" diye sorabilirsiniz.)
4.  "Denemek için bir soru seçin:" bölümündeki örneklere tıklayarak chatbot'u hızlıca test edebilirsiniz.

---

## 🎯 Projenin Amacı ve Çözdüğü Problem

**Problem:** İnsanlar, alışkanlıklarını değiştirme, motivasyonlarını artırma veya erteleme gibi davranışsal zorluklarla karşılaştıklarında, bu durumların arkasındaki bilimsel gerçeklere genellikle karmaşık ve akademik bir dille ulaşırlar. Bu bilgileri anlamak ve günlük hayata uygulamak zordur.

**Amaç:** Bu projeyle, karmaşık nörobilimsel bilgileri, herkesin anlayabileceği, pratik ve eyleme geçirilebilir tavsiyelere dönüştüren bir "koç" kimliğinde yapay zeka asistanı geliştirmek hedeflenmiştir. Chatbot, bilimsel bir temele dayanarak güvenilir cevaplar sunarken, kullanıcıyla empatik ve destekleyici bir diyalog kurar.

---

## 📚 Veri Seti

Projenin bilgi bankası olarak Hugging Face platformunda yer alan **`sydonayrex/fineweb-edu-neuroscience`** veri seti kullanılmıştır.

*   **İçerik:**  Bu veri seti, yüksek kaliteli Fineweb-EDU koleksiyonundan, "neuroscience" (nörobilim) ve "educational psychology" (eğitim psikolojisi) anahtar kelimeleriyle filtrelenerek oluşturulmuştur. Veri seti, toplam 25,944 satırdan oluşmakta ve her bir satır, bir web sayfasından veya eğitim materyalinden alınmış zengin bir İngilizce metin parçası (extract) içermektedir.
*   **Seçim Nedeni:** Akademik makaleler, blog yazıları ve eğitim materyallerinden oluşan bu çeşitli içerik, projenin konusu olan motivasyon, alışkanlıklar ve beyin fonksiyonları hakkında derinlemesine ve güvenilir bir bilgi temeli sunmaktadır.
*   **Hazırlık Metodolojisi:** Veri setindeki bu 25,944 metin parçası, LangChain'in RecursiveCharacterTextSplitter aracı kullanılarak, RAG mimarisinin verimli bir şekilde işleyebileceği yaklaşık 300,000 adet daha küçük ve anlamlı alt parçaya (chunk) bölünmüştür

---

## 🛠️ Çözüm Mimarisi ve Kullanılan Teknolojiler

Proje, Büyük Dil Modelleri'nin (LLM) halüsinasyon riskini ortadan kaldırmak ve cevapları doğrulanabilir bir bilgi kaynağına dayandırmak amacıyla **RAG (Retrieval Augmented Generation)** mimarisi üzerine kurulmuştur.

**Çalışma Akışı:**
1.  Kullanıcının sorusu alınır ve dili tespit edilir.
2.  Soru, arama yapılabilmesi için İngilizce'ye çevrilir.
3.  `all-mpnet-base-v2` modeli ile soru bir vektöre dönüştürülür.
4.  `ChromaDB` vektör veritabanında bu soruyla anlamsal olarak en alakalı metin parçaları bulunur.
5.  Bulunan metinler, sohbet geçmişi ve kullanıcının orijinal sorusu, `Gemini` modeline özel bir prompt şablonu ile gönderilir.
6.  `Gemini`, bu bağlama dayanarak, kullanıcının sorduğu dilde ve "koç" kimliğinde bir cevap üretir.

**Teknoloji Yığını:**
*   **Uygulama Çatısı:** LangChain
*   **Dil Modeli (LLM):** Google Gemini 2.5 Flash
*   **Embedding Modeli:** `sentence-transformers/all-mpnet-base-v2` (Hugging Face)
*   **Vektör Veritabanı:** ChromaDB
*   **Web Arayüzü:** Gradio

---

## ⚙️ Kodun Çalışma Kılavuzu

Bu projenin kodlarını kendi ortamınızda çalıştırmak için aşağıdaki adımları izleyebilirsiniz.

1.  **Repoyu Klonlama:**
    ```bash
    git clone https://github.com/[KULLANICI_ADINIZ]/[REPO_ADINIZ].git
    cd [REPO_ADINIZ]
    ```

2.  **Gerekli Kütüphaneleri Kurma:**
    Projenin çalışması için gereken tüm kütüphaneler `requirements.txt` dosyasında listelenmiştir.
    ```bash
    pip install -r requirements.txt
    ```

3.  **API Anahtarını Ayarlama:**
    Proje, Google Gemini API'sini kullanmaktadır. Bir Google API anahtarı almanız ve bunu `Neuroscience_Chatbot_FINAL.ipynb` not defterinin çalıştığı ortamda (örneğin Colab Secrets) `GOOGLE_API_KEY` adıyla kaydetmeniz gerekmektedir.

4.  **Projeyi Çalıştırma:**
    *   `Neuroscience_Chatbot_FINAL.ipynb` not defterini bir Jupyter ortamında (Google Colab, VS Code vb.) açın.
    *   Not defterindeki Markdown açıklamalarını takip ederek hücreleri sırayla çalıştırın.
    *   **Not:** Bölüm 2 (Bilgi Bankasının İnşası) çalıştırılmamalıdır. Proje, daha önce oluşturulmuş ve Google Drive'da saklanan hazır veritabanını kullanacak şekilde tasarlanmıştır.

---

## 📊 Elde Edilen Sonuçlar ve Geliştirme Süreci

*   **Başarı:** Proje sonucunda, hedeflenen tüm yeteneklere sahip (RAG, hafıza, çok dillilik, web arayüzü) bir chatbot başarıyla geliştirilmiştir.
*   **Zorluklar ve Öğrenilenler:** Geliştirme sürecinde, özellikle `langchain` ekosistemindeki kütüphaneler arasında yaşanan versiyon uyumsuzlukları (`dependency conflicts`) nedeniyle ciddi zorluklarla karşılaşılmıştır. Bu sorunlar, kütüphaneleri doğru sırada kurma, versiyonları sabitleme ve en sonunda `langchain[google-genai]` gibi doğru kurulum yöntemlerini kullanma gibi adımlarla metodik bir şekilde aşılmıştır. Bu süreç, bir projenin temelini oluşturan ortam kurulumunun ne kadar kritik olduğunu göstermiştir.
