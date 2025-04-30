# YZM304 2. Ödev - Derin Öğrenme ile Görüntü Sınıflandırma: CNN ve Hibrit Yöntem Karşılaştırması


## Giriş

Görüntü sınıflandırma, bilgisayarla görme alanının temel problemlerinden biridir. Derin öğrenmenin gelişmesiyle birlikte evrişimli sinir ağları (CNN) bu alanda yüksek başarılar göstermiştir. Bu çalışmada, MNIST ve CIFAR-10 veri setleri üzerinde klasik CNN mimarileri ile hibrit bir yöntemin (özellik çıkarımı + geleneksel makine öğrenmesi) karşılaştırması yapılmıştır. Amaç, farklı mimarilerin doğruluk, hata, eğitim süresi gibi kriterler açısından karşılaştırmalı analizini sunmaktır.

---

## Yöntem

### Veri Setleri

- **MNIST:** 28x28 gri tonlamalı el yazısı rakamlar (0-9)
- **CIFAR-10:** 32x32 renkli görüntüler, 10 sınıf (uçak, araba, kuş, kedi, vs.)

### Kullanılan Modeller

| Model No | Model Adı                     | Açıklama |
|----------|-------------------------------|----------|
| 1        | LeNet-5 (MNIST)               | Klasik CNN, 2 konvolüsyon + 3 tam bağlı katman |
| 2        | Geliştirilmiş LeNet (MNIST)   | Batch Normalization ve Dropout içeren CNN |
| 3        | VGG16 (CIFAR-10)              | Transfer learning, son katman CIFAR-10’a göre düzenlendi |
| 4        | Hibrit Model (CIFAR-10)       | VGG16 ile çıkarılan özellikler → SVM |
| 5        | Tam CNN (CIFAR-10)            | VGG16 modeli tam uçtan uca eğitildi |

### Hibrit Yöntem (Model 4)

1. CIFAR-10 veri seti, VGG16 modeline giriş olarak verildi.
2. `avgpool` katmanından özellikler çıkarıldı.
3. Bu vektörler `.npy` dosyaları olarak kaydedildi.
4. SVM, KNN ve Random Forest gibi modellerle sınıflandırma yapıldı.

### Performans Metodolojisi

- Tüm modeller için `accuracy`, `confusion matrix`, `loss/accuracy grafikleri` hesaplandı.
- Eğitim sonrası test doğrulukları kaydedildi.
- Eğitimler `Adam` optimizer ile 10 epoch boyunca yapılmıştır.
- Cross entropy loss fonksiyonu kullanılmıştır.

---

## Sonuçlar

### Doğruluk Değerleri

| Model                  | Veri Seti | Test Doğruluğu (%) |
|------------------------|-----------|---------------------|
| LeNet-5                | MNIST     | 98.10               |
| Geliştirilmiş LeNet    | MNIST     | 98.87               |
| VGG16 (Tam CNN)        | CIFAR-10  | 86.45               |
| Hibrit (VGG16 + SVM)   | CIFAR-10  | 83.27               |

### Karmaşıklık Matrisi (Confusion Matrix)

Hibrit Model (CIFAR-10) – SVM sınıflandırıcı için:

[[98 0 0 ...]
 [ 0 97 1 ...]
 ...

### Kayıp (Loss) ve Doğruluk (Accuracy) Grafikleri

> Eğitim süresince loss ve accuracy değerleri matplotlib ile görselleştirilmiştir. (Ekteki grafikler GitHub deposundadır.)

---

## Tartışma

Sonuçlar göstermektedir ki klasik CNN mimarileri MNIST veri seti üzerinde oldukça yüksek doğruluklara ulaşabilmektedir. Geliştirilmiş LeNet-5 modeli, Batch Normalization ve Dropout katmanları sayesinde daha stabil ve yüksek başarımlı hale gelmiştir.  
CIFAR-10 veri seti üzerinde VGG16 tabanlı tam CNN modeli, hibrit yaklaşıma kıyasla daha yüksek doğruluk sağlamıştır. Ancak hibrit model, geleneksel makine öğrenmesi algoritmaları ile de başarılı sonuçlar vermiştir. Bu durum, büyük modellerin eğitim süresi ve kaynak gereksiniminden kaçınılması gereken durumlarda hibrit yöntemlerin uygun bir alternatif olabileceğini göstermektedir.

> Not: Eğitim süresi, bellek kullanımı gibi kriterlerde hibrit model daha avantajlı olmuştur. Ancak tam CNN modelleri genellikle doğruluk açısından üstünlük göstermiştir.

---

## Referanslar

1. LeCun, Y., Bottou, L., Bengio, Y., & Haffner, P. (1998). Gradient-based learning applied to document recognition. *Proceedings of the IEEE*.
2. Krizhevsky, A. (2009). Learning Multiple Layers of Features from Tiny Images (CIFAR-10 dataset).
3. Simonyan, K., & Zisserman, A. (2014). Very deep convolutional networks for large-scale image recognition. *arXiv preprint arXiv:1409.1556*.
4. PyTorch Resmi Belgeleri: https://pytorch.org/docs/stable/index.html
5. Scikit-learn Documentation: https://scikit-learn.org/stable/

---
