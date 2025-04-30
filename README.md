# YZM304 2. Ödev - Derin Öğrenme ile MNIST Veri Seti Sınıflandırma

## Giriş

Bu çalışmanın amacı, derin öğrenme yöntemlerinden biri olan konvolüsyonel sinir ağları (CNN) kullanarak, MNIST veri seti üzerinde el yazısı rakamlarını sınıflandırmaktır. MNIST veri seti, 28x28 piksel boyutlarında, 10 farklı rakamı içeren 60,000 eğitim ve 10,000 test örneğinden oluşmaktadır. Derin öğrenme modelleri, özellikle görüntü işleme alanında yüksek doğruluk oranları sağlamakta ve bu çalışma, CNN mimarisinin bu alandaki başarısını test etmeyi hedeflemektedir.

CNN, görsel verileri işlemek için tasarlanmış bir yapay sinir ağı türüdür ve genellikle evrişim (convolution), havuzlama (pooling) ve tam bağlantılı (fully connected) katmanlar içerir. Bu ağ yapısı, görüntüdeki önemli özellikleri öğrenerek, görüntü sınıflandırma gibi görevlerde yüksek performans elde edilmesini sağlar.

## Metod

### Veri Seti
Çalışmada, MNIST veri seti kullanılmıştır. Bu veri seti, el yazısı rakamları içeren 28x28 piksel boyutlarında gri tonlamalı görüntülerden oluşur. Veri seti, eğitim ve test olmak üzere iki bölüme ayrılmıştır. Eğitim verisi 60,000 örnek içerirken, test verisi 10,000 örnekten oluşmaktadır.

### Model Mimarisi
Çalışmada kullanılan model, aşağıdaki katmanları içeren bir CNN mimarisine dayanmaktadır:

1. **Conv1**: İlk evrişim katmanı, 32 filtre ile 3x3 boyutlarında kernel kullanarak giriş görüntüsünü işler.
2. **Conv2**: İkinci evrişim katmanı, 64 filtre ile 3x3 boyutlarında kernel kullanarak daha derin özellikler çıkarır.
3. **Conv3**: Üçüncü evrişim katmanı, 128 filtre ile 3x3 boyutlarında kernel kullanarak daha karmaşık özellikler öğrenir.
4. **MaxPooling**: Her evrişim katmanından sonra max pooling işlemi uygulanarak görüntü boyutu küçültülür ve önemli özellikler seçilir.
5. **Fully Connected Layers**: Evrişim işlemlerinin ardından, öğrenilen özellikler tam bağlantılı katmanlara iletilir ve sınıflandırma yapılır.

Modelin son katmanında, 10 nöronlu bir çıkış katmanı bulunur. Bu çıkış katmanı, 10 rakam sınıfını (0'dan 9'a kadar) temsil eder. Eğitim sırasında, Adam optimizasyonu ve CrossEntropyLoss kayıp fonksiyonu kullanılmıştır.

### Eğitim Süreci
Model, 5 epoch boyunca eğitim verilmiştir. Her epoch sonunda doğruluk oranı ve kayıp değeri hesaplanarak, modelin performansı izlenmiştir. Eğitim verisi üzerinde modelin başarısı, doğruluk oranı ile değerlendirilmiştir.

### Test Süreci
Eğitim süreci tamamlandıktan sonra, modelin genel doğruluğu test veri seti üzerinde ölçülmüştür. Ayrıca, modelin başarısı karmaşıklık matrisi (confusion matrix) ve kayıp grafiği ile görselleştirilmiştir.

## Sonuçlar

### Eğitim Sonuçları
- **Eğitim Doğruluğu**: %98.2
- **Test Doğruluğu**: %97.6

### Karmaşıklık Matrisi
Modelin test verisi üzerindeki performansını gösteren karmaşıklık matrisi aşağıdaki gibidir:





### Kayıp Grafiği
Modelin eğitim sürecinde kayıp fonksiyonunun nasıl değiştiğini gösteren grafik aşağıdaki gibidir:





## Tartışma

Çalışmada kullanılan CNN modeli, MNIST veri setinde oldukça yüksek doğruluk oranları elde etmiştir. Eğitim doğruluğu %98.2, test doğruluğu ise %97.6 olarak ölçülmüştür. Bu sonuç, CNN'nin görüntü sınıflandırma problemlerinde başarılı bir performans sergileyebileceğini göstermektedir.

Modelin doğruluk oranları yüksek olmakla birlikte, farklı model mimarileri (örneğin, daha derin CNN modelleri veya Transfer Learning yöntemleri) kullanılarak performansın daha da iyileştirilmesi mümkündür. Ayrıca, veri artırma (data augmentation) gibi yöntemlerle eğitim setinin çeşitlendirilmesi, modelin genelleme kapasitesini artırabilir.

Bunun dışında, modelin doğruluk oranını etkileyen başka faktörler de mevcuttur. Örneğin, öğrenme oranı, batch size, epoch sayısı gibi hiperparametrelerin ayarlanması, modelin başarısını daha da artırabilir. Ayrıca, modelin test doğruluğunun düşmesi, overfitting (aşırı uyum sağlama) gibi problemlerin ortaya çıkabileceğini göstermektedir. Bu nedenle, modelin daha büyük veri setleriyle eğitilmesi ve farklı doğrulama yöntemlerinin uygulanması, doğruluk oranlarını iyileştirebilir.

## Referanslar

- LeCun, Y., Bottou, L., Bengio, Y., & Haffner, P. (1998). Gradient-based learning applied to document recognition. *Proceedings of the IEEE*, 86(11), 2278-2324.
- He, K., Zhang, X., Ren, S., & Sun, J. (2016). Deep residual learning for image recognition. *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition*, 770-778.
- Krizhevsky, A., Sutskever, I., & Hinton, G. E. (2012). ImageNet classification with deep convolutional neural networks. *Advances in Neural Information Processing Systems*, 1097-1105.
- Chollet, F. (2015). Keras. https://github.com/fchollet/keras
