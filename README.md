Tabii! İşte senin için **tüm README.md** dosyasının kısa, net ve kullanıma hazır hâli:

---

# Kamu Geri Bildirimi ve Duygu Analizi – Test

Bu paket, fine-tune edilmiş **TURKCELL/Turkcell-LLM-7b-v1** modelini HPC üzerinde JSON verileri ile test etmek için hazırlanmıştır.

---

## Gereksinimler

Python 3.9+ ve gerekli kütüphaneler. Tüm bağımlılıkları `requirements.txt` üzerinden yükleyebilirsiniz:

```bash
pip install -r /arf/scratch/teknogrp8u5/final/model/requirements.txt
```

> Not: Yeni bir virtual environment veya HPC ortamı kullanmanız önerilir.

---

## Test Adımları

Test dosyasını çalıştırmak için:

```bash
python /arf/scratch/teknogrp8u5/final/model/test.py \
  --input /arf/scratch/teknogrp8u5/dataset_path.json \
  --text-field yorum \
  --output /arf/scratch/teknogrp8u5/final/model/test_output.json
```

**Parametreler:**

* `--input` → Test etmek istediğiniz JSON veri dosyası
* `--text-field` → Modelin analiz edeceği metin alanı (örn: `yorum`)
* `--output` → Tahminlerin kaydedileceği JSON dosyası

---

## Örnek Dataset

Datasetimiz her geri bildirimi bir JSON nesnesi olarak içerir. Önemli alanlar:

* **`id`** → Geri bildirimin benzersiz numarası
* **`yorum`** → Kullanıcının şikayet veya öneri metni (model bu alan üzerinden duygu analizi yapar)
* **`konu`** → Geri bildirimin başlığı veya konusu
* **`duygu`** → Geri bildirimin etiketi (`negatif`, `nötr`, `pozitif`)
* **`tarih`, `kurum`, `konum`, `kaynak`** → Ek bilgi alanları

**Örnek kayıt:**

```json
{
  "id": "1",
  "yorum": "Çoğu gece mahallede park yeri aramak zorunda kalıyorum...",
  "konu": "İstanbul Büyükşehir Belediyesi Mahallede Park Sorunu",
  "duygu": "negatif",
  "tarih": "10/12/2024",
  "kurum": "İ̇bb-İstanbul",
  "konum": "İstanbul",
  "kaynak": "X"
}
```

---

## Test Çıktısı Örneği

Konsol çıktısı:

```
Metin: Belirli açılış ve kapanış saatleri aralığında hizmet veriyor.
Tahmin: nötr
```

JSON çıktısı `test_output.json` dosyasında saklanır:


* **`id`** → Geri bildirimin benzersiz numarası
* **`yorum`** → Kullanıcının şikayet veya öneri metni (model bu alan üzerinden duygu analizi yapar)
* **`konu`** → Geri bildirimin başlığı veya konusu
* **`duygu`** → Geri bildirimin etiketi (`negatif`, `nötr`, `pozitif`)
* **`tarih`**, **`kurum`**, **`konum`**, **`kaynak`** → Ek bilgi alanları
* **`_pred_label`** → Modelin tahmin ettiği duygu etiketi
* **`_pred_text`** → Modelin tahmin için kullandığı metin


```json
{
    "id": "10000",
    "yorum": "Belirli açılış ve kapanış saatleri aralığında hizmet veriyor.",
    "konu": "Genel",
    "kaynak": "Sentetik",
    "tarih": "02/09/2022",
    "kurum": "Çay Bahçesi – Moda Sahili",
    "konum": "İstanbul",
    "duygu": "nötr",
    "_pred_label": "nötr",
    "_pred_text": "Belirli açılış ve kapanış saatleri aralığında hizmet veriyor."
  }
```





---

