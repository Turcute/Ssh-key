# GitHub İçin Birden Fazla SSH Anahtarı Kullanma Rehberi

Bu rehberde, birden fazla GitHub hesabı için ayrı SSH anahtarları oluşturma, GitHub'a ekleme ve kullanma adımları anlatılmaktadır.

---

## 🚀 1. SSH Anahtarlarını Oluşturma

Öncelikle terminali açın ve aşağıdaki adımları takip edin.

### ✨ İlk hesap için SSH anahtarı oluşturun
```sh
ssh-keygen -t ed25519 -C "ilk.email@example.com"
```
**Dosya adını şu şekilde belirleyin:**
```sh
Enter file in which to save the key (/home/kullanici/.ssh/id_ed25519): ~/.ssh/id_ed25519_hesap1
```

### ✨ İkinci hesap için SSH anahtarı oluşturun
```sh
ssh-keygen -t ed25519 -C "ikinci.email@example.com"
```
**Dosya adını şu şekilde belirleyin:**
```sh
Enter file in which to save the key (/home/kullanici/.ssh/id_ed25519): ~/.ssh/id_ed25519_hesap2
```

---

## 🛠 2. SSH Yapılandırmasını Güncelleme

SSH yapılandırmasını düzenlemek için aşağıdaki komutu çalıştırın:
```sh
touch ~/.ssh/config
nano ~/.ssh/config
```
Açılan dosyaya aşağıdaki satırları ekleyin:
```ini
# İlk GitHub hesabı
Host github.com-hesap1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_hesap1

# İkinci GitHub hesabı
Host github.com-hesap2
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_hesap2
```
**Dosyayı kaydedin ve çıkın.** (Nano kullanıyorsanız: `CTRL + X`, sonra `Y` ve `Enter`)

SSH dosya izinlerini düzenleyin:
```sh
chmod 600 ~/.ssh/config
```

---

## 🔑 3. SSH Anahtarlarını GitHub'a Ekleme

Aşağıdaki komutlarla her iki hesabın **public key**'ini görüntüleyin ve GitHub'a ekleyin.

### 📋 İlk hesap için SSH public key'i alın
```sh
cat ~/.ssh/id_ed25519_hesap1.pub
```
Bu çıktıyı **GitHub → Settings → SSH and GPG keys → New SSH Key** kısmına ekleyin.

### 📋 İkinci hesap için SSH public key'i alın
```sh
cat ~/.ssh/id_ed25519_hesap2.pub
```
Bunu da **ikinci GitHub hesabınıza** ekleyin.

---

## 🔄 4. SSH Bağlantısını Test Etme
Aşağıdaki komutlarla SSH bağlantılarınızı test edin:
```sh
ssh -T github.com-hesap1
ssh -T github.com-hesap2
```
Başarılı bir bağlantı için şu mesajı almalısınız:
```
Hi [kullanıcı_adı]! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 📂 5. Projelerde Kullanıcı Ayarlarını Yapılandırma

Her proje için Git bilgilerini aşağıdaki gibi ayarlayın:

### 🏗 İlk hesap için bir proje klasöründe
```sh
cd /proje/klasoru

git config user.name "İlk Hesap İsmi"
git config user.email "ilk.email@example.com"
```

### 🏗 İkinci hesap için başka bir proje klasöründe
```sh
cd /diger/proje/klasoru

git config user.name "İkinci Hesap İsmi"
git config user.email "ikinci.email@example.com"
```

---

## 🔗 6. Projeleri Klonlama

### 🛠 İlk hesap için
```sh
git clone git@github.com-hesap1:kullanici1/repo.git
```

### 🛠 İkinci hesap için
```sh
git clone git@github.com-hesap2:kullanici2/repo.git
```

Eğer daha önce bir proje klonlandıysa, aşağıdaki komutla **remote adresini değiştirebilirsiniz**:
```sh
git remote set-url origin git@github.com-hesap1:kullanici1/repo.git
```
veya
```sh
git remote set-url origin git@github.com-hesap2:kullanici2/repo.git
```

---

## 🎯 Sonuç
Bu rehberde, **birden fazla GitHub hesabı için SSH anahtarları oluşturma, GitHub'a ekleme ve kullanma** işlemleri detaylı bir şekilde anlatıldı. Artık her iki hesabı da sorunsuz bir şekilde kullanabilirsiniz! 🚀

