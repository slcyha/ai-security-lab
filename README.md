LOCAL Aİ SECURİTY LAB KURULUMU

Bu repoda, yapay zeka güvenliği ve LLM zafiyetlerini (Prompt Injection vb.) test etmek için kurduğum yerel laboratuvarın adım adım kurulum sürecini ve karşılaştığım engelleri nasıl aştığımı paylaşıyorum. Projede Damn Vulnerable AI Application (DVAIA) ve Docker altyapısını kullandım.

ÖN HAZIRLIK

Projeyi çalıştırmak için önce şu iki aracı kurdum:

*Git: İnternetteki repoları terminalden çekebilmek için. (git-scm.com)

*Docker Desktop: Lab ortamını bilgisayarıma zarar vermeden, izole bir konteyner içinde çalıştırmak için.
 
YAŞADIĞIM SORUNLAR VE ÇÖZÜMLERİ 
**YAŞADIĞIM SORUNLAR VE ÇÖZÜMLERİ**

Sistemi sıfırdan kurarken ufak pürüzlerle karşılaştım. Sonradan kuracaklar için notlar:

*   **Sanallaştırma Hatası:** Docker ilk açılışta donanımsal sanallaştırmanın kapalı olduğunu söyledi. Bilgisayarın BIOS ayarlarına girip Intel VT-X / AMD-V (SVM Mode) özelliğini aktif hale getirerek çözdüm.
*   **WSL 2 Eksikliği:** Windows altyapısının Linux konteynerlerini çalıştırabilmesi için gerekli olan WSL eksikti. Yönetici yetkisiyle açtığım PowerShell'de şu komutu çalıştırıp bilgisayarı yeniden başlattım:
    ```powershell
    wsl --install
    ```
*   **Eksik .env Dosyası:** Docker'ı ilk ayağa kaldırmaya çalıştığımda `.env` dosyasını bulamadığı için hata verdi. Klasör içindeki örnek şablonu kopyalayarak gerekli çevre dosyasını oluşturdum.

ADIM ADIM KURULUM
**ADIM ADIM KURULUM**

Projeyi kendi bilgisayarınızda çalıştırmak için izlenecek adımlar:

1. **Repoyu klonlayın ve klasöre girin:**
   ```bash
   git clone [https://github.com/KULLANICI_ADINIZ/REPO_ADINIZ.git](https://github.com/KULLANICI_ADINIZ/REPO_ADINIZ.git)
   cd REPO_ADINIZ
   
Çevre dosyasını hazırlayın:

PowerShell
Copy-Item .env.example .env

Docker ile ayağa kaldırın:

PowerShell
docker compose up -d
Test ortamına gidin:
İşlem bitince tarayıcıdan http://localhost:5000 adresine girerek arayüze ulaşabilirsiniz.
```markdown
**HEDEFLENEN GÜVENLİK TESTLERİ**

Bu laboratuvar ortamı başarıyla izole edildikten sonra, aşağıdaki LLM zafiyetleri üzerine ofansif güvenlik testleri gerçekleştirilecektir:
*   **Prompt Injection:** Modelin orijinal talimatlarını manipüle etme.
*   **Jailbreak:** Güvenlik filtrelerini aşarak sınırlandırılmış yanıtları tetikleme.
*   **Information Disclosure:** Modelin eğitim verisinde kalmış olabilecek hassas bilgileri sızdırma denemeleri.

<img width="860" height="418" alt="Ekran görüntüsü 2026-07-20 180927" src="https://github.com/user-attachments/assets/1573d43b-87d7-4f99-b7fa-a193287577e4" />

<img width="872" height="379" alt="Ekran görüntüsü 2026-07-20 182906" src="https://github.com/user-attachments/assets/a0904f45-933e-4655-847c-86bb1edbbb1d" />

<img width="1270" height="620" alt="Ekran görüntüsü 2026-07-20 180903" src="https://github.com/user-attachments/assets/119fdc72-4604-4632-ac94-7d271ff9cf14" />
