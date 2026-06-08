# deepfake-detection-dsf-ext
Deepfake Görüntü Tespiti Projesi (Makine Öğrenmesi)
# Deepfake Görüntü Tespiti — DSF_Ext


## Proje Özeti
Bu çalışmada FaceForensics++ (FF++) C23 veri seti üzerinde eğitilen,
frekans ve uzamsal öznitelikleri çapraz dikkat mekanizmasıyla birleştiren
DSF_Ext (Deepfake detection with Spatial-Frequency Extended) modeli
geliştirilmiştir. Temel DSF mimarisine Çapraz-Dikkat Füzyon Modülü (CAFM),
yardımcı sınıflandırma başlığı (AuxHead) eklenmiştir.

## Veri Seti
| | Eğitim | Doğrulama | Test |
|---|:---:|:---:|:---:|
| Fake video (her tür) | 180 | 20 | 50 |
| Toplam fake video | 720 | 80 | 200 |
| Real video | 720 | 80 | 200 |
| Manipülasyon türleri | Deepfakes, Face2Face, FaceSwap, NeuralTextures | | |

- Bölme video bazlı yapılmıştır (frame sızıntısı önlendi)
- Her videodan 10 frame alınmıştır
- Cross-dataset testi: Celeb-DF
- Cross-manipulation testi: DeepFakeDetection (DFD)

## Model Mimarisi
- Omurga: ConvNeXt-Base (ImageNet ön eğitimli)
- Frekans dalları: DWT (Haar wavelet) + DCT (YCbCr, 8×8 blok)
- CAFM: 4 başlı çift yönlü çapraz dikkat
- AuxHead: FCEM çıkışında bağımsız sınıflandırıcı
- Eğitim: 25 epoch, AdamW, Warmup + Cosine Annealing

## Sonuçlar
| Test Senaryosu             | Veri Seti| AUC    |
--------------------------------------------------
| İntra-dataset              | FF++ C23 | 0.9080 |
| Cross-dataset              | Celeb-DF | 0.6382 | 
| Cross-manipulation (frame) | DFD      | 0.8428 | 
| Cross-manipulation (video) | DFD      | 0.9093 | 


## Gereksinimler
- Python 3.10+
- PyTorch 2.0+
- timm, pytorch_wavelets, scikit-learn

## Referanslar
Tüm literatür referansları RIS formatında `references.zip`
dosyasında mevcuttur.

## Dosya Yapısı
├── notebook/
│   └── dsf_ext.ipynb        # Eğitim ve test kodu
├── report/
│   └── rapor.pdf            # Proje raporu
├── references.zip           # Literatür referansları (RIS)
└── README.md
