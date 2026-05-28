# Özel Telegram Drive 📁

Bu proje, dosyalarınızı doğrudan kişisel Telegram hesabınıza yedeklemenizi sağlayan, tamamen tarayıcı üzerinde çalışan modern ve hafif bir "Cloud Drive" arayüzüdür. Dosyalarınız Telegram sunucularında güvenle saklanır, geçmiş kayıtlarınız ise Firebase Realtime Database üzerinde tutulur.

## 🚀 Özellikler
* Sürükle-bırak desteği ile kolay dosya yükleme.
* Resimler için otomatik önizleme.
* Modern ve mobil uyumlu arayüz.
* Telegram bot API'si üzerinden sınırsız dosya depolama (Telegram'ın dosya boyutu limitleri dahilinde).

---

## 🛠️ Kurulum Rehberi

Bu projeyi kendi ortamınızda çalıştırmak için kendi **Telegram Bot** bilgilerinizi ve **Firebase** veritabanınızı bağlamanız gerekmektedir. 

Aşağıdaki adımları izleyerek `index.html` içindeki gerekli yerleri doldurun.

### Adım 1: Telegram Bot Token Alma
1. Telegram'ı açın ve arama kısmına **@BotFather** yazın.
2. BotFather'a `/newbot` mesajını gönderin.
3. Botunuz için bir isim ve kullanıcı adı belirleyin.
4. BotFather size bir **HTTP API Token** verecektir. (Örn: `123456789:ABCdefGHIjklmNOPqrstuVWXyz`).
5. Bu kodu kopyalayın ve `index.html` dosyasındaki şu satıra yapıştırın:
   ```javascript
   const botToken = "YOUR_TELEGRAM_BOT_TOKEN"; 


### Adım 2: Telegram Chat ID Alma

Botun dosyaları size gönderebilmesi için sizin Chat ID'nize ihtiyacı vardır.

1. Yeni oluşturduğunuz botu Telegram'da bulup **Başlat** (/start) butonuna basın. (Bu çok önemlidir, aksi takdirde bot size mesaj gönderemez).
2. Chat ID'nizi öğrenmek için Telegram'da **@userinfobot** veya **@RawDataBot** gibi bir bota mesaj gönderin.
3. Bot size `Id: 123456789` şeklinde bir numara verecektir.
4. Bu numarayı kopyalayın ve `index.html` dosyasındaki şu satıra yapıştırın:
```javascript
const userChatId = "YOUR_TELEGRAM_CHAT_ID";
  ```



### Adım 3: Firebase Kurulumu (Geçmişi Kaydetmek İçin)

Yüklediğiniz dosyaların listesini tarayıcıda görebilmek için Firebase veritabanı kullanılır.

1. [Firebase Console](https://console.firebase.google.com/)'a gidin.
2. Yeni bir proje oluşturun.
3. Proje panosunda "Web" (</>) ikonuna tıklayarak yeni bir web uygulaması ekleyin.
4. Ekrana gelen `firebaseConfig` kod bloğunu kopyalayın ve `index.html` içindeki aynı isimli objenin içine yapıştırın:
```javascript
const firebaseConfig = {
  apiKey: "YOUR_FIREBASE_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT_ID-default-rtdb.firebaseio.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT_ID.firebasestorage.app",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};

```


5. Firebase sol menüden **Realtime Database**'e tıklayın ve veritabanı oluşturun.
6. **Kurallar (Rules)** sekmesine gidin ve okuma/yazma izinlerini test amaçlı geçici olarak açın:
```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}

```


*(Not: Bu ayar veritabanınızı herkese açık hale getirir. Projeyi sadece yerel bilgisayarınızda (localhost) veya kendinize özel güvenli bir sunucuda çalıştırın.)*

### Adım 4: Çalıştırın!

Her şey hazır! Sadece `index.html` dosyasına çift tıklayarak tarayıcınızda açın ve ilk dosyanızı yükleyin.

## ⚠️ Uyarılar
* Bu proje istemci tarafında (client-side) çalışır. HTML kodunu herkese açık bir internet sitesine (Örn: GitHub Pages, Cloudflare Pages, Vercel vb.) yüklerseniz, kaynak kodunuzdaki Telegram Token'ı ve Firebase API anahtarları herkes tarafından görülebilir.
* Projeyi veri güvenliğiniz için **sadece yerel bilgisayarınızda (çevrimdışı veya localhost)** kullanmanız şiddetle tavsiye edilir.
