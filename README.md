# Flip 7 🃏

Tarayıcıda oynanan, tek dosyalık (self-contained) bir **Flip 7** kart oyunu. Aynı cihazda sırayla (hotseat) oynanabilir ya da Firebase Realtime Database üzerinden **online odalar** kurup arkadaşlarınla gerçek zamanlı oynayabilirsin.

Canlı demo: `index.html` dosyasını açman yeterli — kurulum, derleme adımı ya da sunucu gerektirmez.

## Özellikler

- **Tek dosya, framework yok** — sade HTML + CSS + vanilla JavaScript.
- **Hotseat modu** — 2-8 oyuncu aynı cihazda sırayla oynar.
- **Online mod** — Firebase Realtime Database ile oda kur/katıl, gerçek zamanlı senkronize oyun.
  - Oda kodu ile davet, host/misafir/izleyici rolleri.
  - Sırası gelmeyen oyuncu hamle yapamaz; host tüm oyun mantığını yönetir, diğer istemciler durumu izler.
  - Bağlantı koparsa (`onDisconnect`) oyuncu/oda otomatik temizlenir.
- **Oda içi sohbet** — Her odanın kendine ait, ayrı bir sohbet kanalı vardır; bir odadaki mesajlar başka bir odada görünmez ve host odadan ayrılınca oda ile birlikte silinir. İzleyicilerin mesajlarının yanında **(izleyici)** etiketi gösterilir.
- **Kart uçuşma animasyonu**, tur özeti, kazanan ekranı, sağ üstte oyunu bitir / odadan ayrıl butonları.
- **Mobil öncelikli tasarım**, `prefers-reduced-motion` desteği.

## Oyun kuralları (özet)

Her oyuncu sırayla desteden kart çeker; elindeki sayı kartlarında **tekrar varsa** oyundan elenir (bust). Elindeki 7 farklı sayı kartını toplayan oyuncu o turu anında +15 bonusla kazanır. `Dondur`, `Üç Çek` ve `İkinci Şans` gibi özel aksiyon kartları, `+N` ve `×2` modifikatör kartları bulunur. İlk 200 puana ulaşan oyuncu oyunu kazanır.

## Nasıl çalıştırılır

Herhangi bir kurulum gerekmez:

1. Bu depoyu klonla veya indir.
2. `index.html` dosyasını bir tarayıcıda aç.

Hotseat modu bu şekilde doğrudan çalışır. Online mod için internet bağlantısı ve Firebase servislerine erişim (gstatic.com, firebaseio.com) gerekir.

### GitHub Pages ile yayınlama

1. Depoyu GitHub'a yükle (bu README'nin yanına `index.html` dosyasını da ekle).
2. **Settings → Pages** bölümünden `main` dalını (branch) kaynak olarak seç.
3. Birkaç dakika içinde `https://<kullanici-adi>.github.io/<repo-adi>/` adresinden erişilebilir olur.

## Online mod için kendi Firebase projeni kurmak

Depodaki `index.html` içinde hazır bir Firebase yapılandırması bulunuyor. Kendi kopyanı barındıracaksan (özellikle herkese açık bir repo/sitede), kendi Firebase projeni oluşturup `firebaseConfig` nesnesini değiştirmen önerilir:

1. [Firebase Console](https://console.firebase.google.com/)'da yeni bir proje oluştur.
2. **Build → Realtime Database**'i etkinleştir (test modunda başlayabilirsin, sonra kuralları sıkılaştır).
3. **Build → Authentication**'da **Anonymous** (anonim) giriş yöntemini etkinleştir — oyun her ziyaretçiye anonim bir kimlik atar.
4. Proje ayarlarından bir **Web App** ekle ve sana verilen yapılandırma nesnesini kopyala.
5. `index.html` içindeki `firebaseConfig` bloğunu (yaklaşık 416. satır) kendi bilgilerinle değiştir:

   ```js
   const firebaseConfig = {
     apiKey: "...",
     authDomain: "...",
     databaseURL: "...",
     projectId: "...",
     storageBucket: "...",
     messagingSenderId: "...",
     appId: "..."
   };
   ```

6. Realtime Database kurallarını oda/sohbet verisi için uygun şekilde ayarla (örnek — sadece giriş yapmış kullanıcılar okuyup yazabilsin):

   ```json
   {
     "rules": {
       "rooms": {
         "$code": {
           ".read": "auth != null",
           ".write": "auth != null"
         }
       }
     }
   }
   ```

> Not: Firebase web `apiKey` değeri gizli bir sır değildir (istemci tarafında zaten görünür durumdadır), asıl güvenlik **Realtime Database kuralları** ile sağlanır. Kendi projeni kullanmak istemiyorsan depodaki hazır yapılandırmayla da online mod çalışır, ancak paylaşılan bir proje olduğu için kapasite/kota sınırlamalarına takılabilir.

## Proje yapısı

```
.
├── index.html   # Oyunun tamamı (HTML + CSS + JS) tek dosyada
└── README.md
```

## Katkı

Sorun bildirimleri ve pull request'lere açığız. Değişiklik yapmadan önce bir issue açman, tartışmayı kolaylaştırır.

## Lisans

Bu proje için bir lisans dosyası henüz eklenmedi. Depoyu kullanmadan/dağıtmadan önce bir `LICENSE` dosyası eklemen önerilir (ör. MIT).
