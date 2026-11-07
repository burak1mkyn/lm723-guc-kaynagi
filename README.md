# LM723 Tabanlı Ayarlanabilir DC Güç Kaynağı

LM723 entegresi ve harici güç transistörü ile tasarlanmış, ayarlanabilir çıkış gerilimli ve akım sınırlamalı lineer DC güç kaynağı. Proteus'ta simüle edildi, şeması ve PCB'si EasyEDA Pro'da çizildi.

## Durum

- [x] Proteus simülasyonu
- [x] EasyEDA Pro şeması ve PCB tasarımı
- [x] Üretim dosyaları (Gerber) hazır
- [ ] PCB üretimi ve montaj
- [ ] Gerçek ölçümler ve test sonuçları

## Tasarım Hedefleri

| Özellik | Hedef |
|---|---|
| Çıkış gerilimi | Ayarlanabilir, yaklaşık 30 V'a kadar |
| Akım sınırı | Yaklaşık 3 A |
| Giriş | Trafo + köprü diyot + 4700 µF filtre kondansatörü |

Not: Değerler tasarım hesabıdır. Kart üretilip test edildikten sonra ölçülen değerler buraya eklenecek.

## Çalışma Prensibi

LM723, içindeki yaklaşık 7,15 V'luk referans gerilimini ve hata yükselteciyle çıkışı sabit tutar. Potansiyometre referans gerilimini bölerek yükseltecin eviren olmayan girişine uygular. Çıkıştan alınan geri besleme, 33 kΩ ve 10 kΩ'luk bölücüyle eviren girişe gider ve çıkış gerilimi yaklaşık olarak şu orana göre ayarlanır:

`Vout ≈ Vref_ayarlı × (1 + 33k / 10k)`

LM723 tek başına küçük akım verebildiği için çıkış akımını harici bir NPN güç transistörü (şemada 2N3055) taşır. Akım sınırlama, çıkışa seri bağlı 0,22 Ω'luk algılama direncinin üzerindeki gerilim düşümüyle yapılır. LM723'ün akım sınırlama eşiği yaklaşık 0,65 V olduğu için:

`I_sınır ≈ 0,65 V / 0,22 Ω ≈ 3 A`

## Devre ve PCB

![Proteus şeması](sematik/proteus-sema.png)
![EasyEDA şeması](sematik/easyeda-sema.png)
![PCB 3D görünüm](goruntuler/pcb-3d.png)

## Malzeme Listesi

| Parça | Değer / Model |
|---|---|
| U1 | LM723 (DIP-14) |
| Q1 | NPN güç transistörü (şemada 2N3055) |
| D1 | Köprü diyot [model ve akım değeri] |
| C1 | 4700 µF elektrolitik [gerilim değeri] |
| R (akım algılama) | 0,22 Ω, en az 5 W |
| R (geri besleme) | 33 kΩ ve 10 kΩ |
| Potansiyometre | 10 kΩ |
| TR1 | [trafo ikincil gerilimi ve akımı] |
| Klemensler | Giriş ve çıkış için 2 adet |

## Klasör Yapısı

- `sematik/` şema görselleri
- `simulasyon/` Proteus proje dosyası
- `pcb/` EasyEDA proje dosyası ve Gerber (üretim) dosyaları
- `goruntuler/` PCB 3D görünümü ve kart fotoğrafları

## Bu Projede Öğrendiklerim

- Lineer regülatör mantığı: referans, hata yükselteci ve geri besleme
- Güç transistörü ile akım artırma ve akım sınırlama devresi
- Aynı devreyi hem op-amp (TL081) hem LM723 ile tasarlayıp karşılaştırma
- Şemadan PCB'ye, üretim dosyalarına kadar tasarım akışı

## Araçlar

Proteus, EasyEDA Pro

## İletişim

Burak Mükyen, [LinkedIn](https://www.linkedin.com/in/burak-mükyen-5a503a381)
