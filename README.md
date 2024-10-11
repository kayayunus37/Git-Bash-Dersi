# Git Bash

## 1. Git Nedir?

Git, dağıtık bir versiyon kontrol sistemidir. Projendeki kod değişikliklerini izlemene ve yönetmene yardımcı olur. Git ile, projenin farklı sürümlerini kaydedebilir, geri alabilir, işbirliği yapabilir ve hata yaptığında eski versiyonlara dönebilirsin.

---

## 2. Git Kurulumu

Git’i kurduktan sonra, Git Bash kullanarak komutları terminal üzerinde çalıştırabilirsin. İlk olarak Git’i yapılandırman gerekiyor.

**a. Kullanıcı Adı ve E-posta Ayarları**

Proje üzerinde kimlik bilgilerinle işlem yapabilmen için Git, kullanıcı adını ve e-posta adresini bilmelidir. Bu bilgiyi şöyle ayarlayabilirsin:
```
git config --global user.name "Adın Soyadın"
git config --global user.email "email@example.com"
```
--global parametresi, bu ayarların tüm Git projelerin için geçerli olacağı anlamına gelir. Her projede farklı bilgiler kullanmak istersen, bu komutu o projede --global olmadan çalıştırabilirsin.

**b. Git Ayarlarını Görüntüleme**

Yaptığın ayarları kontrol etmek istersen:
`git config --list`

---

## 3. Yeni Bir Depo (Repository) Oluşturma

**a. Yerel Bir Depo Oluşturma**

Bir proje için yeni bir Git deposu oluşturmak istiyorsan, proje klasörüne gidip git init komutunu kullanabilirsin. Bu, o klasörde Git ile proje takibi yapmana olanak tanır.
```
cd (Klasör dizini)
git init
```
Bu adımlarla boş bir Git deposu oluşturmuş olursun. .git adlı gizli bir klasör oluşur ve burada proje sürümlerine dair kayıtlar tutulur.

**b. Mevcut Bir Depoyu Klonlama**

GitHub gibi uzak bir depo (remote repository) üzerinde bulunan bir projeyi bilgisayarına almak istiyorsan git clone komutunu kullanırsın.

`git clone https://github.com/kullanici/proje-adi.git`

---

## 4. Git’te Temel İş Akışı

Git ile çalışma sürecinde genellikle şu üç adım tekrar edilir:

**a. Dosya Ekleme ve Düzenleme**

Projende yeni dosyalar ekleyebilir veya mevcut dosyalarda değişiklik yapabilirsin. Örneğin, Yazılarım.txt adında bir dosya oluşturalım:

`echo "# Proje Başlığı" > Yazılarım.txt`

**b. Dosyaları “Staging Area”ya Ekleme**

Yaptığın değişiklikleri Git’e bildirmek için onları “staging area”ya eklemen gerekiyor. Bu işlem için git add komutunu kullanırsın:

`git add Yazılarım.txt`

Eğer tüm değişiklikleri eklemek istiyorsan: `git add .`

**c. Değişiklikleri Commit Etme**

Staging area’ya eklediğin dosyaları bir commit ile kaydedersin. Commit, değişikliklerin kaydedildiği bir sürüm noktasıdır.

`git commit -m "Yazılarım.txt eklendi"`

Bu işlem, proje geçmişine yaptığın değişiklikleri ekler. -m parametresi ile kısa bir açıklama mesajı yazarsın.

---

## 5. Branch (Dal) Kullanımı

Branch, projede paralel geliştirme yapmanı sağlar. Varsayılan olarak main (eski adıyla master) dalında çalışırsın. Yeni bir özellik geliştirmek veya hata düzeltmek için yeni bir dal (branch) oluşturabilirsin.

**a. Yeni Bir Branch Oluşturma ve Geçiş Yapma**

Yeni bir dal oluşturup ona geçiş yapmak için:

`git checkout -b yeni-ozellik`

Bu komut, yeni-ozellik adında bir dal oluşturur ve bu dala geçiş yapar. Bu dalda çalışırken, ana dal (main) ile çakışmadan yeni özellikler geliştirebilirsin.

**b. Dallar Arasında Geçiş**

Dallar arasında geçiş yapmak için git checkout komutunu kullanırsın:

`git checkout main`

**c. Uzak Dala Göndermek ve Eşleştirmek**

Aşağıdaki komutu kullanarak new_feature dalını uzak depoya gönderirken aynı zamanda bu dalı upstream olarak ayarlayabilirsin:

`git push --set-upstream origin new_feature`

Bu komut:

- origin: Uzak depoyu temsil eder (varsayılan ad).
- new_feature: Göndermek istediğin yerel dalın adıdır.

Bu komut çalıştırıldığında, new_feature dalı uzak depoya yüklenecek ve bu dalın upstream olarak ayarlanacaktır.

**d. Önceden Uzak Dala Bağlama**

Alternatif olarak, git push komutunu kullanmadan önce, mevcut dalı uzak dal ile ilişkilendirmek için aşağıdaki komutu da kullanabilirsin:
```
git branch --set-upstream-to=origin/new_feature
git push
```

**e. Branch’leri Birleştirme (Merge)**

Geliştirdiğin özelliği ana dal ile birleştirmek için:

1. Ana dala (main) geri dön: `git checkout main`
2. Değişiklikleri birleştir: `git merge yeni-ozellik`

---

## 6. Uzak Depolar (Remote Repositories)

Git, projeni GitHub gibi uzak bir depoya göndermene (push) veya oradan güncellemeleri çekmene (pull) izin verir.

**a. Uzak Depoyu Ekleme**

Bir projeye uzak bir depo eklemek için şu komutu kullanabilirsin:

`git remote add origin https://github.com/kullanici/proje-adi.git`

**b. Değişiklikleri Uzak Depoya Gönderme (Push)**

Yerel depodaki değişiklikleri uzak depoya göndermek için git push komutunu kullanırsın:

`git push origin main`

**c. Uzak Depodan Değişiklikleri Çekme (Pull)**

Uzak depodaki en son değişiklikleri almak için:

`git pull origin main`

---

## 7. Pull Request (PR)

GitHub gibi platformlarda başkalarının projelerine katkı yapmak istediğinde Pull Request açarsın. PR, senin önerdiğin değişikliklerin, proje sahibi tarafından gözden geçirilip projeye eklenmesini talep eder.

**a. Pull Request Nasıl Yapılır?**

1. Yeni bir branch oluşturup değişikliklerini yap.
2. Branch’ini uzak depoya gönder: `git push origin yeni-branch`
3. GitHub’da projeye git ve “New Pull Request” butonuna tıkla. Değişikliklerini gözden geçirip PR’yi aç.

---

## 8. Git’in Diğer Temel Komutları

**a. Durum Kontrolü**

Git deposunun durumunu görmek için git status komutunu kullan:
`git status`

Bu komut, hangi dosyaların değiştirildiğini, hangilerinin staging area’da olduğunu ve hangi branch’te çalıştığını gösterir.

**b. Commit Geçmişini Görüntüleme**

Yapılan commit’leri görmek için:

`git log`

Bu komut, tüm commit geçmişini gösterir. Daha kısa bir özet görmek istersen:

`git log --oneline`

**c. Commitleri Geri Alma**

Bir commit’i geri almak istiyorsan:

- Son commit’i geri almak (Değişiklikler kalır):

  `git reset --soft HEAD~1`

- Son commit’i tamamen geri almak (Değişiklikler de silinir):
  `git reset --hard HEAD~1`

---

## 9. Git ile İşbirliği

Bir ekip içinde çalışırken Git’in branch, pull ve push gibi özellikleri çok önemlidir. Özellikle büyük projelerde hatasız çalışmak ve takım arkadaşlarının yaptığı değişikliklerle çakışmadan geliştirme yapabilmek için branch kullanımına dikkat etmelisin. Ayrıca, düzenli olarak commit yapmak ve açıklayıcı commit mesajları yazmak, projeni daha anlaşılır ve takip edilebilir hale getirir.

---

## 10. GitHub Actions ve CI/CD

GitHub, projelerde otomatik testler ve dağıtımlar için GitHub Actions özelliğini sunar. CI/CD (Continuous Integration/Continuous Deployment) süreçleriyle, kodun her güncellenmesinde otomatik testler çalıştırılabilir ve başarılı olursa yeni sürümler dağıtılabilir.
