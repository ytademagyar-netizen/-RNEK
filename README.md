# Cloudstream Depom

## Kurulum (baştan sona)
1. GitHub'da **public** yeni bir depo aç (örn. `cloudstream-depom`).
2. Bu klasördeki tüm dosyaları depoya yükle (ana dal `main` veya `master`).
3. **KULLANICI** ve **DEPO** yazan yerleri değiştir:
   `repo.json`, `build.gradle.kts`, `OrnekEklenti/build.gradle.kts`.
4. Depoda *Settings → Actions → General → Workflow permissions* → **Read and write permissions** → Save.
5. Push yapınca *Actions* sekmesi derlemeyi çalıştırır; sonunda `builds` dalında `.cs3` ve `plugins.json` oluşur.
6. Cloudstream → *Ayarlar → Uzantılar → Depo ekle* → şu adresi yapıştır:
   `https://raw.githubusercontent.com/KULLANICI/DEPO/main/repo.json`
   (dal adın `master` ise `main` yerine `master` yaz). Ya da kısaca `KULLANICI/DEPO` yazmayı dene.
7. Eklentiyi listeden indir.

## Yeni eklenti eklemek
`OrnekEklenti` klasörünü kopyala, yeniden adlandır, içindeki `namespace`, paket adı ve
sınıf adlarını değiştir. `settings.gradle.kts` klasörü otomatik bulur.

## Güncelleme
Kodu değiştirince eklentinin `build.gradle.kts` içindeki `version` değerini artır ve push et.

## Domain yakalama
`OrnekProvider.kt` domain değişimini otomatik yakalar:
- `domain.txt` (depo kökünde, satır başına bir adres) önce okunur. Domain değişirse sadece bu dosyayı güncelle ve push et; eklentiyi yeniden derlemen gerekmez.
- Dosya okunamazsa koddaki `yedekDomainler` listesi denenir.
- Yönlendirmeler takip edilir, son adres `mainUrl` olur; eski domain'li kayıtlı linkler yeni domain'e çevrilir.
- `domainDosyasi` içindeki `KULLANICI/DEPO` kısmını değiştirmeyi unutma.
