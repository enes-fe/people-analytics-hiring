# People Analytics: Teknik İşe Alım Krizi Analizi

## Problem
Bir manufacturing firmasında teknik rollerde (Technician, Planner, QualityInspector, Maintenance) işe alım süreci bozuldu:

- **Time-to-fill:** 39 günden 71 güne çıktı (+82%)
- **Early attrition:** İlk 6 ayda ayrılma oranı %26.3
- **Offer acceptance:** Agency kaynaklı adaylarda sadece %5.3

Bu proje, sorunun **nerede** ve **neden** yaşandığını veriye dayalı olarak ortaya koyuyor ve operasyonel aksiyon önerileri sunuyor.

---

## Yaklaşım

Gerçek şirket verisi bulunmadığından sentetik veri üretildi. Veri üretimi sırasında aşağıdaki gerçekçi senaryolar simüle edildi:

- Son 6 ayda işe alım aşamaları arası gecikmenin artması
- Agency kaynağında offer decline ve early attrition'ın yüksek olması
- Belirli yöneticilerin ekiplerinde overtime ve attrition'ın birlikte yükselmesi
- Eğitim tamamlamayan çalışanlarda erken ayrılma riskinin artması

---

## Veri Seti

| Dosya | Açıklama | Satır |
|-------|----------|-------|
| `data/recruitment.csv` | Aday bazlı işe alım süreci | 900 |
| `data/employee.csv` | Çalışan bazlı performans ve attrition | 350 |

**Önemli not:** Veri tamamen sentetiktir. Tüm isimler, tarihler ve metrikler Python ile üretilmiştir. Gerçek bir şirket verisini temsil etmez.

---

## Analizler

### 1. Recruitment Funnel
900 başvurudan 234'ü işe alındı (%26). En büyük kayıp son aşamada — teklif alan 504 kişinin sadece %46'sı işe başladı. Bu teklif'te veya son süreçte sıkıntı olabileceğini gösterir.

### 2. Time-to-Fill Decomposition
| Aşama | Önceki 12 Ay | Son 6 Ay | Artış |
|-------|-------------|----------|-------|
| Applied→Screen | 7 gün | 11 gün | +4 gün |
| Screen→Interview | 14 gün | 21.5 gün | +7.5 gün |
| Interview→Offer | 6 gün | 12 gün | +6 gün |
| Offer→Start | 15 gün | 26 gün | +11 gün |

En kritik gecikme: **Offer→Start (+11 gün)** ve **Screen→Interview (+7.5 gün)**

### 3. Early Attrition Analizi
- Eğitim almayan çalışanlarda attrition: **%46.5**
- Eğitim alan çalışanlarda attrition: **%19.7**
- M002 ve M003 yöneticilerinde attrition: **%40-50** (overtime 85-89 saat)

### 4. Kaynak Analizi (Source)
| Kaynak | Hired Oranı | Offer Decline |
|--------|------------|---------------|
| Referral | %33 | %6 |
| LinkedIn | %33 | %8 |
| Agency | %3 | %27 |

---

## Aksiyon Önerileri

| Bulgu | Aksiyon | Beklenen Etki |
|-------|---------|---------------|
| Screen→Interview gecikmesi | Haftada 2 sabit mülakat günü + recruiter performans analizi | Time-to-fill ~-%20 |
| Offer→Start gecikmesi | Dijital onboarding süreci + Teklif analizine göre tekliflerin iyileştirilmesi | Time-to-fill ~-%10 |
| Agency offer decline %27 | Referral/University kaynaklarını güçlendirme | Offer acceptance ~+%15 |
| Eğitimsizlerde attrition %46 | İlk 30 günde eğitim zorunluluğu | Early attrition ~-%30 |
| M002/M003/M004/M011 riski | Yönetici koçluğu ve ekip anketi + M002 ve M003 için overtime sürelerinin dengelenmesi | Risk altındaki 120 çalışan'ın riski azalır |

---

## Repo Yapısı

```
├── data/
│   ├── recruitment.csv
│   ├── employee.csv
│   ├── funnel.png
│   ├── ttf_decomposition.png
│   └── attrition_analysis.png
├── notebooks/
│   ├── 01_generate_data.ipynb
│   └── 02_analysis.ipynb
└── README.md
```

---

## Kullanılan Teknolojiler

- Python 3.13
- pandas, numpy
- matplotlib, seaborn
- Faker (sentetik veri üretimi)

---

## Kısıtlamalar ve Varsayımlar

- Veri sentetiktir — gerçek şirket dinamiklerini tam yansıtmayabilir
- Gecikme parametreleri manuel olarak ayarlandı, gerçek kalibrasyona ihtiyaç duyar
- Yönetici etkisi korelasyon bazlı gözlemlenmiştir, nedensellik iddia edilmemektedir
- Early attrition için 180 gün eşiği kullanıldı, sektör standardı farklılık gösterebilir
