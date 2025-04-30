# YZM304 2. Ödev - Derin Öğrenme ile Görüntü Sınıflandırma: CNN ve Hibrit Yöntem Karşılaştırması

## Giriş

Görüntü sınıflandırma, bilgisayarla görme alanının temel problemlerinden biridir. Derin öğrenmenin gelişmesiyle birlikte evrişimli sinir ağları (CNN) bu alanda yüksek başarılar göstermiştir. Bu çalışmada, **MNIST** ve **CIFAR10** veri setleri üzerinde klasik CNN mimarileri ile hibrit bir yöntemin (özellik çıkarımı + geleneksel makine öğrenmesi) karşılaştırması yapılmıştır. Amaç, farklı mimarilerin doğruluk, hata, eğitim süresi gibi kriterler açısından karşılaştırmalı analizini sunmaktır.

---

## Klasör Yapısı ve Açıklamaları

| Klasör/Dosya Adı             | Açıklama |
|-----------------------------|----------|
| `LeNet5`                    | MNIST veri seti için klasik LeNet-5 CNN mimarisi |
| `ImprovedLeNet5`            | Batch Normalization ve Dropout içeren geliştirilmiş LeNet-5 modeli |
| `LeNet5_train_test`         | LeNet5 eğitimi ve testi için ana betik |
| `ImprovedLeNet5_epoch`      | Geliştirilmiş LeNet5 modeli için epoch bazlı doğruluk/kayıp görselleştirme |
| `mnist_loader_and_plot`     | MNIST veri yükleme ve sonuç görselleştirme araçları |
| `CIFAR10_train`             | CIFAR10 için model eğitimi (özellikle VGG16 temelli) |
| `CIFAR10_test`              | CIFAR10 veri seti üzerinde test işlemi |
| `CIFAR10`                   | CIFAR10 veri ön işleme ve temel işlemler |
| `CIFAR10_VGG16`             | Transfer learning kullanarak eğitilen VGG16 modeli (özellik çıkarımı için) |
| `CIFAR10_VGG16_Full`        | Uçtan uca tamamen eğitilen VGG16 CNN modeli |
| `extract_features`          | VGG16'nin `avgpool` katmanından özellik çıkarımı işlemleri |
| `SVM`                       | Hibrit model için SVM sınıflandırıcısının uygulanması |

---

## Yöntem

### Veri Setleri

- **MNIST:** 28x28 gri tonlamalı el yazısı rakamlar (0-9)
- **CIFAR10:** 32x32 renkli görüntülerden oluşan 10 sınıf (uçak, araba, kuş, kedi, vs.)

### Kullanılan Modeller

| Model No | Model Adı                 | Veri Seti | Açıklama |
|----------|---------------------------|-----------|----------|
| 1        | `LeNet5`                  | MNIST     | Klasik CNN: 2 konvolüsyon + 3 tam bağlı katman |
| 2        | `ImprovedLeNet5`          | MNIST     | Batch Normalization ve Dropout içeren CNN |
| 3        | `CIFAR10_VGG16_Full`      | CIFAR10   | Transfer learning ile uçtan uca eğitilen VGG16 |
| 4        | `CIFAR10_VGG16` + `SVM`   | CIFAR10   | VGG16 ile çıkarılan özelliklerle SVM sınıflandırma |
| 5        | `CIFAR10_VGG16`           | CIFAR10   | VGG16 özellikleri  |

---

## Hibrit Yöntem (Model 4)

1. `CIFAR10_VGG16` ile VGG16 modeline CIFAR10 görüntüleri verildi.
2. `extract_features` betiği ile `avgpool` katmanından vektör çıkarımı yapıldı.
3. Bu vektörler `.npy` dosyalarına kaydedildi.
4. `SVM` klasörü içinde yer alan kodlar ile sınıflandırma gerçekleştirildi.

---

## Performans Değerlendirme

- `accuracy`, `confusion matrix`, `loss/accuracy` grafik çıktıları her model için kaydedildi.
- Tüm modeller `Adam` optimizer ve `CrossEntropyLoss` ile eğitildi (10 epoch).
- `ImprovedLeNet5_epoch` ve `mnist_loader_and_plot` dosyaları eğitim süreci görselleştirmeleri içindir.


## Sonuçlar

- **Model 1: LeNet-5**'in doğruluğu %96.93 olarak ölçülmüştür.
- **Model 2: ImprovedLeNet5**'in doğruluğu %98.09'a çıkmıştır.
- **Model 3: CIFAR10_VGG16_Full**'in doğruluğu %87.58 ile daha düşük kalmıştır.
- **Model 4: CIFAR10_VGG16 + SVM**'in doğruluğu %98.83 olmuştur.
- **Model 5: CIFAR10_VGG16 + Diğer (KNN / Random Forest)** ise %98.89 ile en yüksek doğruluğu sağlamıştır.

---

## Tartışma

Sonuçlar, klasik CNN mimarilerinin MNIST gibi sade veri setlerinde çok yüksek başarı sağladığını göstermektedir. Geliştirilmiş LeNet5 modeli, Batch Normalization ve Dropout kullanımı ile daha stabil ve başarılı bir model olmuştur.  
CIFAR10 gibi daha karmaşık veri setlerinde, uçtan uca eğitilen VGG16 modeli hibrit modele göre daha yüksek doğruluk vermiştir. Ancak hibrit model, geleneksel yöntemlerle de iyi sonuçlar elde ederek düşük kaynak ihtiyacı olan sistemlerde avantajlı hale gelmektedir.

> Eğitim süresi ve kaynak kullanımı açısından hibrit model oldukça verimlidir. Ancak doğruluk açısından tam eğitilmiş CNN'ler genel olarak daha üstündür.

---

## Referanslar

1. LeCun, Y., et al. (1998). *Gradient-based learning applied to document recognition*, Proceedings of the IEEE.
2. Krizhevsky, A. (2009). *Learning Multiple Layers of Features from Tiny Images*.
3. Simonyan, K., & Zisserman, A. (2014). *Very deep convolutional networks for large-scale image recognition*. arXiv:1409.1556.
4. [PyTorch Belgeleri](https://pytorch.org/docs/stable/)
5. [Scikit-learn Belgeleri](https://scikit-learn.org/stable/)
