# Perakende Bankacılık için PD Tabanlı Kredi Riski Erken Uyarı Modeli
> ⚠️ **Önemli:** Analizi düzgün görüntülemek için pdf yerine `pd-early-warning-model.ipynb` dosyasını açınız. Veya `pd-early-warning-model.html` dosyasını kaydederek de tarayıcınız üzerinden görüntüleyebilirsiniz.

Bu projede perakende bankacılık kredi portföyü için **12 aylık temerrüt olasılığını (Probability of Default – PD)** tahmin eden ve bu tahminleri kullanarak **erken uyarı (Early Warning) ve risk segmentasyonu** üreten bir model geliştirilmiştir.

Model, müşterileri temerrüt riskine göre sıralayarak risk ekiplerinin operasyonel olarak kullanabileceği bir **watchlist yaklaşımı** oluşturmayı amaçlamaktadır. Böylece sınırlı operasyon kapasitesinin en riskli müşterilere yönlendirilmesi mümkün hale gelir.

---

# İş Problemi

Bankalarda risk ekipleri tüm kredi portföyünü tek tek inceleyemez. Bu nedenle yüksek riskli müşterilerin erken tespit edilmesi ve sınırlı operasyon kapasitesinin doğru müşterilere yönlendirilmesi gerekir.

Bu projede geliştirilen model:

- Müşteriler için temerrüt olasılığı tahmini üretir
- Müşterileri risk seviyesine göre sıralar
- Operasyonel olarak kullanılabilecek **erken uyarı (watchlist) segmentasyonu** oluşturur

---

# Modelleme Yaklaşımı

Model **lojistik regresyon** kullanılarak kurulmuştur. Modelin amacı her müşteri için **0 ile 1 arasında bir temerrüt olasılığı (PD)** tahmini üretmektir.

Bağımsız değişkenler hem müşteri davranışını hem de makroekonomik koşulları temsil edecek şekilde seçilmiştir.

Kullanılan temel değişkenler:

- dti
- utilization
- past_due_30d_count
- income
- salary_customer
- product_count
- policy_rate
- unemployment
- cpi_yoy

---

# Model Performans Analizi

Model performansı çeşitli metrikler kullanılarak değerlendirilmiştir.

## Modelin Ayırma Gücü

Modelin temerrüt eden ve etmeyen müşterileri ayırt edebilme yeteneği aşağıdaki metriklerle analiz edilmiştir:

- ROC Curve
- AUC (Area Under Curve)
- Kolmogorov–Smirnov (KS) İstatistiği

Bu metrikler modelin **discrimination power** olarak adlandırılan ayırma gücünü ölçmektedir.

## Risk Sıralama Performansı

Modelin yüksek riskli müşterileri portföyün üst sıralarında toplayabilme başarısı aşağıdaki analizlerle incelenmiştir:

- Decile analizi
- Capture rate
- Lift curve

Bu analizler modelin **riskli müşterileri yoğunlaştırma performansını** değerlendirmek için kullanılmıştır.

---

# Eşik (Threshold) Analizi

Model çıktıları farklı eşik değerleri kullanılarak değerlendirilmiş ve her eşik için:

- Confusion matrix
- Precision
- Recall
- F1-score

metrikleri hesaplanmıştır.

Temerrüt modellemesinde özellikle **riskli müşterilerin kaçırılmaması (Recall)** kritik öneme sahiptir. Ancak operasyonel verimlilik açısından yanlış alarm oranı da dikkate alınmıştır.

---

# Watchlist Yaklaşımı

Bankalarda operasyon ekipleri genellikle tüm portföy yerine **portföyün en riskli kısmına odaklanır**. Bu nedenle pratik uygulamalarda sabit bir eşik yerine genellikle **Top %X yaklaşımı** kullanılır.

Bu projede model çıktıları kullanılarak:

- RED segment (yüksek risk)
- AMBER segment (orta risk)
- GREEN segment (düşük risk)

şeklinde bir **risk segmentasyonu** oluşturulmuştur.

---

# Capture ve Lift Analizi

Modelin yüksek riskli müşterileri ne kadar iyi yakalayabildiğini değerlendirmek için:

- Capture rate
- Lift curve

analizleri yapılmıştır.

Bu analizler modelin operasyonel erken uyarı sistemi olarak kullanılabilirliğini değerlendirmek açısından önemlidir.

---

# Backtesting ve Stabilite Analizi

Model performansının zaman içerisinde tutarlı olup olmadığını incelemek amacıyla **aylık bazda AUC ve kalibrasyon analizi** yapılmıştır.

Bu analiz modelin farklı dönemlerde de benzer performans gösterdiğini doğrulamak için kullanılmıştır.

---

# Kullanılan Kütüphaneler

Projede aşağıdaki Python kütüphaneleri kullanılmıştır:

- pandas
- numpy
- scikit-learn
- statsmodels
- matplotlib

---

# Sonuç

Geliştirilen model kredi portföyündeki müşterileri temerrüt riskine göre sıralayabilmekte ve yüksek riskli müşterileri erken aşamada tespit edebilmektedir.

Model çıktıları kullanılarak oluşturulan risk segmentasyonu, bankalarda kullanılan erken uyarı ve watchlist sistemlerine benzer bir operasyonel yaklaşım sunmaktadır.

Bu çalışma kredi riski modellemesi ve veri bilimi tekniklerinin bankacılık uygulamalarında nasıl kullanılabileceğini gösteren örnek bir projedir.
