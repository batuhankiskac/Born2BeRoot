# Debian Rehberi

Projenin **Debian** sürümü için rehber.

`bkiskac` olarak giriş yapın ve ardından `root` olarak giriş yaparak `vim` kurulumunu yapın.

```bash
su - # root kullanıcısına geçiş
apt-get install vim
```

Herhangi bir paketin kurulumunu doğrulamak için:

```bash
dpkg -l | grep $PACKAGE_NAME
```

Terminal üzerinden sistemi kapatmak için:

```bash
shutdown -f now
```

---

## 1 - `sudo` Kurulumu ve Kullanıcıyı Gruba Ekleme

```bash
apt-get install sudo
sudo adduser bkiskac sudo
sudo reboot
sudo -v # Kullanıcıyı doğrular: Komut çalıştırmadan zaman damgasını günceller
sudo addgroup user42
sudo adduser bkiskac user42
sudo apt-get update
```

**Not:** Kullanıcının **sudo** grubuna başarıyla eklenip eklenmediğini doğrulayın:

```bash
getent group sudo
```

---

## 2 - SSH Kurulumu ve Yapılandırması

1. SSH sunucusunu kurun ve yapılandırma dosyasını düzenleyin:

```bash
sudo apt-get install openssh-server
sudo vi /etc/ssh/sshd_config
```

- `#Port 22` satırını `Port 4242` olarak değiştirin.
- `#PermitRootLogin prohibit-password` satırını `PermitRootLogin no` olarak değiştirin.

2. **`sshd_config` ve `ssh_config` Farkı:**
   - `sshd_config`: Sunucu yapılandırmasını belirler.
   - `ssh_config`: İstemci yapılandırmasını belirler.

```bash
sudo vi /etc/ssh/ssh_config
```

- `#Port 22` satırını `Port 4242` olarak değiştirin.

3. Değişikliklerin etkinleşmesi için sistemi yeniden başlatın:

```bash
sudo reboot
sudo service ssh status
```

4. VirtualBox'ta port yönlendirme kuralını `4242:4242` olarak ayarlayın.

5. SSH ile sanal makineye bağlanmak için:

```bash
ssh bkiskac@127.0.0.1 -p 4242
ssh bkiskac@0.0.0.0 -p 4242
ssh bkiskac@localhost -p 4242
```

---

## 3 - UFW (Güvenlik Duvarı) Kurulumu

1. UFW'yi kurun ve etkinleştirin:

```bash
sudo apt-get install ufw
sudo ufw enable
sudo ufw allow 4242
sudo ufw status
```

2. Numaralandırılmış kuralları listelemek için:

```bash
sudo ufw status numbered
```

3. Bir kuralı silmek için:

```bash
sudo ufw delete $NUMBER
```

---

## 4 - `sudo` Yapılandırması

1. `sudo` yapılandırma dosyasını oluşturun ve düzenleyin:

```bash
sudo touch /etc/sudoers.d/sudoconfig
sudo mkdir /var/log/sudo
sudo vi /etc/sudoers.d/sudoconfig
```

2. Dosya içeriği:

```
Defaults    passwd_tries=3
Defaults    badpass_message="Yanlış sudo şifresi, toplamda 3 hakkınız var."
Defaults    log_input,log_output
Defaults    iolog_dir="/var/log/sudo"
Defaults    requiretty
Defaults    secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

---

## 5 - Güçlü Şifre Politikası Belirleme

1. Şifre politikası için yapılandırma dosyasını düzenleyin:

```bash
sudo vi /etc/login.defs
```

- `PASS_MAX_DAYS    99999` → `PASS_MAX_DAYS    30`
- `PASS_MIN_DAYS    0` → `PASS_MIN_DAYS    2`

2. `libpam-pwquality` paketini yükleyin ve yapılandırın:

```bash
sudo apt-get install libpam-pwquality
sudo vi /etc/pam.d/common-password
```

- `password requisite pam_pwquality.so retry=3` satırına şu parametreleri ekleyin:

```
minlen=10 ucredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root
```

3. Şifreleri değiştirin:

```bash
passwd
sudo passwd
```

---

## `cron` ile Zamanlanmış Görevler

1. Bir script dosyası oluşturun ve düzenleyin:

```bash
sudo vi /home/monitoring.sh
```

2. Script'i çalıştırılabilir hale getirin:

```bash
sudo chmod +x /home/monitoring.sh
```

3. Cron görevlerini düzenleyin:

```bash
sudo crontab -u root -e
```

4. Şu satırı ekleyin:

```
*/10 * * * * /home/monitoring.sh
```

5. Zamanlanmış görevleri kontrol edin:

```bash
sudo crontab -u root -l

