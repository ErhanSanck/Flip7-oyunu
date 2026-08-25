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
