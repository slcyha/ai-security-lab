
Local AI Security Lab Kurulum

Bu repoda, yapay zeka güvenliği ve LLM zafiyetlerini (Prompt Injection vb.) test etmek için kurduğum yerel laboratuvarın adım adım kurulum sürecini ve karşılaştığım engelleri nasıl aştığımı paylaşıyorum. Projede Damn Vulnerable AI Application (DVAIA) ve Docker altyapısını kullandım.

## 1. Ön Hazırlık
Projeyi çalıştırmak için önce şu iki aracı kurdum:

*Git: İnternetteki repoları terminalden çekebilmek için. (git-scm.com)
*Docker Desktop: Lab ortamını bilgisayarıma zarar vermeden, izole bir konteyner içinde çalıştırmak için.
 
Kurulum Öncesi Yaşadığım Engeller ve Çözümleri
Sistemi sıfırdan kurarken ufak pürüzlerle karşılaştım. Sonradan kuracaklar için notlar:

Sanallaştırma Hatası:
Docker ilk açılışta donanımsal sanallaştırmanın kapalı olduğunu söyledi. Bilgisayarın BIOS ayarlarına girip Intel VT-X / AMD-V (SVM Mode) özelliğini aktif hale getirerek çözdüm.

WSL 2 Eksikliği:
Windows alt yapısının Linux konteynerlerini çalıştırabilmesi için gerekli olan WSL eksikti. Yönetici yetkisiyle açtığım PowerShell'de şu komutu çalıştırıp bilgisayarı yeniden başlattım:

PowerShell
wsl --install
Eksik .env Dosyası:
Docker'ı ilk ayağa kaldırmaya çalıştığımda .env dosyasını bulamadığı için hata verdi. Klasör içindeki örnek şablonu kopyalayarak gerekli çevre dosyasını oluşturdum.

Adım Adım Kurulum
Projeyi kendi bilgisayarınızda çalıştırmak için izlenecek adımlar:

Repoyu klonlayın:

Bash
git clone https://github.com/KULLANICI_ADINIZ/REPO_ADINIZ.git
cd REPO_ADINIZ
Çevre dosyasını hazırlayın:

PowerShell
Copy-Item .env.example .env
Docker ile ayağa kaldırın:

PowerShell
docker compose up -d
Test ortamına gidin:
İşlem bitince tarayıcıdan http://localhost:5000 adresine girerek arayüze ulaşabilirsiniz.

<img width="860" height="418" alt="Ekran görüntüsü 2026-07-20 180927" src="https://github.com/user-attachments/assets/1573d43b-87d7-4f99-b7fa-a193287577e4" />

<img width="872" height="379" alt="Ekran görüntüsü 2026-07-20 182906" src="https://github.com/user-attachments/assets/a0904f45-933e-4655-847c-86bb1edbbb1d" />
