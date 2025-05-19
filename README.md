# ATM-ve-Online-Bankacilik-Uygulumasi
# Online Bankacılık Ağı ve ATM Simülasyonu

> **Ders:** Bilgisayar Ağları – Proje Final Raporu  
> **Dönem:** 2024‑2025 Bahar  
> **Üniversite:** T.C. Marmara Üniversitesi, Teknoloji Fakültesi, Bilgisayar Mühendisliği Bölümü

## Hazırlayanlar

| İsim | Öğrenci No |
| ---- | ---------- |
| Arif Küçükeşmekaya | 170423049 |
| Şevval Çulcu | 171423961 |
| Ertuğrul Selim Öztürk | 171423011 |

---

## İçindekiler
- [Projenin Amacı](#projenin-amacı)
- [Projede Kullanılan Teknolojiler](#projede-kullanılan-teknolojiler)
- [Projede Neler Yapıldı?](#projede-neler-yapıldı)
- [Projenin Ağ Mimarisi ve Altyapı Kurulumu](#projenin-ağ-mimarisi-ve-altyapı-kurulumu)
- [Sistemin Çalışma Mantığı](#sistemin-çalışma-mantığı)
- [Sonuç ve Değerlendirme](#sonuç-ve-değerlendirme)
- [Projenin Arayüzü](#projenin-arayüzü)
- [Canlı Demo ve Kaynak Kod](#canlı-demo-ve-kaynak-kod)

---

## Projenin Amacı
Bu projede, bilgisayar ağları üzerinde çalışan **bankacılık sistemi** simülasyonu geliştirildi.  
İki ana modül vardır:

1. **ATM Modülü:** Para çekme, para yatırma, borç ödeme  
2. **Online Bankacılık Modülü:** Ek olarak hesaplar arası transfer

Her iki modül de **istemci‑sunucu mimarisi** kullanır; istekler ağ üzerinden sunucuya iletilir, işlemler merkezi olarak yürütülir. Böylece ağ programlama, veri güvenliği ve istemci‑sunucu iletişimi konuları uygulamalı olarak ele alınmıştır. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}

---

## Projede Kullanılan Teknolojiler
- **AWS VPC, Subnet, Internet/NAT Gateway**
- **EC2** (çoklu Availability Zone)
- **Application Load Balancer** + **Auto Scaling**
- **AWS IAM, WAF, Shield**
- **Amazon CloudWatch** (izleme & loglama)
- **Python / Flask** (örnek)  
  <!-- ihtiyaç duyduğun dil/çatıları buraya ekleyebilirsin -->

---

## Projede Neler Yapıldı?
1. **Ağ mimarisi tasarımı** ve VPC oluşturma  
2. Public / Private subnet yapılandırması  
3. Internet & NAT Gateway kurulumu  
4. EC2 örneklerinin dağıtılması  
5. Yük dengeleme ve otomatik ölçeklendirme  
6. Çok katmanlı güvenlik politikalarının eklenmesi  
7. CloudWatch ile izleme ve alarm mekanizmaları  
8. ATM ve Online Bankacılık arayüzlerinin geliştirilmesi

---

## Projenin Ağ Mimarisi ve Altyapı Kurulumu
Aşağıdaki şemada, uygulamanın AWS üzerindeki dağıtımı gösterilmiştir:

<!-- görsel: aws_mimari.png -->

| Katman | Bileşenler | Açıklama |
| ------ | ---------- | -------- |
| **Kamu** | ALB, NAT Gateway | İnternetten gelen trafiğin ilk durağı |
| **Özel** | EC2 (Uygulama), RDS/DB | Kritik servisler korumalı subnet’te |
| **Güvenlik** | IAM, WAF, Shield | Kimlik yönetimi & saldırı koruması |

---

## Sistemin Çalışma Mantığı
```mermaid
sequenceDiagram
    participant Kullanıcı
    participant ALB
    participant EC2
    Kullanıcı->>ALB: HTTP(S) İsteği
    ALB->>EC2: Yönlendirme
    EC2-->>Kullanıcı: JSON/HTML Yanıt


## Sonuç ve Değerlendirme

| Hedef                | Durum | Açıklama                            |
|----------------------|:-----:|-------------------------------------|
| **Yüksek Erişilebilirlik** | ✔️ | Uygulama çoklu AZ’de çalışıyor.      |
| **Güvenlik**         | ✔️ | IAM, WAF ve Shield katmanlı koruma sağlar. |
| **Ölçeklenebilirlik**| ✔️ | ALB + Auto Scaling talebe göre kapasiteyi ayarlar. |
| **Gözlemlenebilirlik** | ✔️ | CloudWatch metrik ve log’lar ile izlenir. |

Bu yapı sayesinde sistem **kesintisiz**, **güvenli** ve **talep artışına dayanıklı** biçimde çalışmaktadır.

## Projenin Arayüzü

### ATM

<img src="screenshots/atm_main.png" alt="ATM Ana Ekran" width="700" />

- **Güncel Bakiye** görüntüler.
- **Para Çek / Para Yatır / Borç Öde** işlemleri.
- Yetersiz bakiye gibi durumlarda kullanıcı dostu uyarılar.

### Online Bankacılık

<img src="screenshots/online_banking.png" alt="Online Bankacılık" width="700" />

- **Para Transferi**, **Yaklaşan Ödemeler** ve **İşlem Geçmişi**.
- Tüm formlarda sunucu‑taraflı doğrulama (kart no, PIN, bakiye vb.).

## Canlı Demo ve Kaynak Kod

| Bağlantı | Açıklama |
|----------|----------|
| **🔗 Canlı Demo** | <http://bank-app.metricopt.com/> |
