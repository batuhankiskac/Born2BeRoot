## **APT && Aptitude**
- **APT (Advanced Package Tool):** Debian tabanlı Linux sistemlerinde kullanılan bir paket yönetim aracıdır. Paketlerin kurulumu, kaldırılması ve yönetimi için temel araçtır.
- **Aptitude:** APT'nin sunduğu özelliklerin çoğunu barındıran, ancak ek özelliklere sahip bir paket yönetim aracıdır. Daha kullanıcı dostu bir arayüz sunar ve özellikle bağımlılık yönetiminde esnek çözümler sunar.

---

## **APT'nin Özellikleri**
1. **Hızlı ve Basit:**
   - Komut satırı üzerinden doğrudan paket yönetimi sağlar.
   - Kullanımı genellikle hızlıdır ve sistemin temel paket yönetim işlevlerini yerine getirir.

2. **Bağımlılık Yönetimi:**
   - APT, paket bağımlılıklarını otomatik olarak çözer ve indirir.
   - Ancak, bağımlılıkları yönetirken kullanıcıya fazla seçenek sunmaz.

3. **Komutlar:**
   - Paket yükleme: `sudo apt install paket_adı`
   - Paket kaldırma: `sudo apt remove paket_adı`
   - Güncelleme: `sudo apt update`

4. **Arayüz:**
   - Sadece komut satırı üzerinden çalışır.

---

## **Aptitude'nin Özellikleri**
1. **Kullanıcı Dostu Arayüz:**
   - Aptitude, hem komut satırı hem de metin tabanlı bir arayüz (TUI) sunar.
   - Metin tabanlı arayüz, paketleri görsel olarak yönetmek isteyen kullanıcılar için kullanışlıdır.

2. **Bağımlılık Yönetiminde Esneklik:**
   - Aptitude, bağımlılık sorunlarıyla karşılaştığında kullanıcıya alternatif çözümler sunar.
   - Örneğin, bir paketin bağımlılığı çözülmezse, bağımlılığı kaldırmayı veya alternatif bir paket yüklemeyi önerir.

3. **Ekstra Fonksiyonlar:**
   - Yüklenmiş paketlerin durumlarını, kullanılmayan paketleri ve bağımlılık sorunlarını daha detaylı şekilde raporlar.

4. **Komutlar:**
   - Paket yükleme: `sudo aptitude install paket_adı`
   - Paket kaldırma: `sudo aptitude remove paket_adı`
   - Güncelleme: `sudo aptitude update`

5. **Arayüz:**
   - TUI modunda başlatmak için: `sudo aptitude`
   - Bu mod, paketlerin listelerini, durumlarını ve bağımlılıklarını görsel olarak inceleme imkânı sunar.

---

## **APT ve Aptitude Arasındaki Farklar**
| Özellik                  | **APT**                          | **Aptitude**                     |
|--------------------------|----------------------------------|-----------------------------------|
| **Kullanım Türü**        | Komut satırı                    | Komut satırı + TUI (Metin arayüzü)|
| **Bağımlılık Yönetimi**  | Temel bağımlılık yönetimi        | Daha esnek bağımlılık seçenekleri|
| **Hız**                  | Daha hızlı                      | TUI kullanıldığında daha yavaş    |
| **Raporlama**            | Basit ve temel                  | Detaylı raporlama ve öneriler     |
| **Kapsam**               | Çoğu kullanıcı için yeterli      | Gelişmiş kullanıcılar için ideal  |

---

## **Hangi Durumlarda Kullanılır?**
- **APT Kullanımı:**
  - Paket yönetimi konusunda hızlı ve basit bir araç gerektiğinde.
  - Daha az bağımlılık çözümleme sorunu olan durumlarda.

- **Aptitude Kullanımı:**
  - Bağımlılık sorunlarının detaylı çözümlenmesi gerektiğinde.
  - TUI arayüzü üzerinden paketleri görsel olarak yönetmek istendiğinde.
  - Sistem durumunun daha detaylı raporlanması gerektiğinde.

---

## **AppArmor Nedir?**
**AppArmor**, Linux sistemlerinde zorunlu erişim kontrolü (Mandatory Access Control - MAC) sağlayan bir güvenlik modülüdür. Sistem yöneticilerinin, belirli uygulamaların sistem kaynaklarına erişimini kısıtlamasına olanak tanır. Bu, bir uygulamanın sadece izin verilen dosyalara, ağ bağlantılarına veya işlemlere erişmesini sağlar.

---

### **AppArmor'ın Temel Özellikleri**
1. **Profil Tabanlı Koruma:**
   - Her uygulama için ayrı bir güvenlik profili oluşturulur.
   - Bu profiller, uygulamaların hangi kaynaklara erişebileceğini belirler.

2. **İki Çalışma Modu:**
   - **Enforce (Zorlayıcı) Mod:**
     - Profiller aktif olarak uygulanır ve izin verilmemiş eylemler engellenir.
   - **Complain (Şikayet) Mod:**
     - Uygulama kısıtlanmaz, ancak ihlaller kaydedilir.

3. **Kolay Yönetim:**
   - Profiller kolayca oluşturulabilir, düzenlenebilir ve devreye alınabilir.

---

### **AppArmor Nasıl Çalışır?**
- Sistem, her uygulama için belirlenmiş bir profil yükler.
- Uygulama, yalnızca profilinde belirtilen işlemleri gerçekleştirebilir.
- Örneğin, bir web sunucusu yalnızca belirli dizinlere erişebilir ve ağ bağlantısı kurabilir.

---

### **AppArmor Kullanımı**
1. **Profil Yönetimi:**
   - Profilleri listelemek için:
     ```bash
     sudo aa-status
     ```
   - Bir uygulama için profil yüklemek:
     ```bash
     sudo aa-enforce /path/to/profile
     ```

2. **Yeni Profil Oluşturma:**
   - Profil oluşturmak için AppArmor'un `aa-genprof` aracı kullanılabilir:
     ```bash
     sudo aa-genprof uygulama_adı
     ```

---

### **AppArmor'ın Avantajları**
1. **Ekstra Güvenlik Katmanı:**
   - Uygulamaların yalnızca ihtiyaç duydukları kaynaklara erişmesini sağlar.

2. **Kolay Yönetim:**
   - Profillerin yönetimi basit ve esnektir.

3. **Kapsamlı İzleme:**
   - Complain modu sayesinde potansiyel sorunları tespit etme imkânı sunar.
