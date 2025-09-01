
# Kamu Geri Bildirimi ve Duygu Analizi – Test

Bu paket, fine-tune edilmiş **TURKCELL/Turkcell-LLM-7b-v1** modelini JSON veri üzerinde test etmek için hazırlanmıştır.



## Gereksinimler

Python 3.9+ ve aşağıdaki kütüphaneler gereklidir. Tüm bağımlılıkları `requirements.txt` dosyasından yükleyebilirsiniz:

```bash
pip install -r /arf/scratch/teknogrp8u5/final/model/requirements.txt
```


## Test Adımları

1. Model ve tokenizer klasörünü indirin:
   
./llm_finetune/final_model


2. Test dosyasını çalıştırın:

/arf/scratch/teknogrp8u5/final/model bu dizin içerisinde kendi datasetinizde dataset_path.json  dosyasını değiştirerek aşağıda bulunan komut ile test işlemlerini gerçekleştirebilirsiniz.

```bash
  python test.py --input /arf/scratch/teknogrp8u5/dataset_path.json --text-field yorum --output /arf/scratch/teknogrp8u5/final/model/test_output.json
```

* `--text-field` → JSON’da metinlerin bulunduğu anahtar (örnek: `yorum`)
* `--output` → Çıktı JSON dosyası
