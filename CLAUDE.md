# CLAUDE.md

## Proje Sahibi
Taha Tokgöz — Offensive Security Researcher | Red Team Operator | OSCP+ Candidate
Marka: ShahMat Sec ♞

## Proje
tahatokgoz.com — Statik kişisel web sitesi. GitHub Pages üzerinden yayınlanıyor.
Domain: tahatokgoz.com (Namecheap DNS, GitHub Pages A kayıtları + CNAME)
Repo: github.com/tahatokgoz/tahatokgoz.com

## Kalite Standardı
- Her zaman yapılabilecek EN ÜST kaliteyi hedefle — ortalama veya "yeterli" kabul edilmez
- Profesyonel, gerçek dünyada rekabet edebilir seviyede olmalı
- Yarım iş bırakma, "sonra ekleriz" deme — o anki adımı tam bitir
- Acımasızca dürüst ol, lafı dolandırma
- Hata olursa "çalışması lazım" gibi belirsiz cümleler kurma, kesin çöz

## Teknoloji Stack
- Saf HTML5 + CSS (inline `<style>` bloğu) + JavaScript
- Tailwind YOK, framework YOK, build step YOK, bundler YOK, paket yöneticisi YOK
- CDN kütüphaneleri (her HTML dosyasının altında):
  - Three.js r128 — particle field arka plan
  - GSAP 3.12.7 + ScrollTrigger — scroll animasyonları
  - Lenis 1.1.18 — smooth scroll
  - Google Fonts — Syne (başlık) + JetBrains Mono (metin/kod)
- Her HTML dosyası tamamen bağımsız (standalone) — kendi CSS ve JS'ini içerir

## Tasarım Sistemi
Aşağıdaki tokenlar HER HTML dosyasında tekrarlanır. Bir token değiştiğinde TÜM dosyalar senkronize edilmeli:

| Token | Değer | Kullanım |
|-------|-------|----------|
| --bg-void | #030303 | Body arka plan |
| --bg-primary | #050505 | Section arka plan |
| --bg-card | #0a0a0a | Kart arka planı |
| --border-subtle | #141414 | İnce border |
| --border-active | #1f1f1f | Hover border |
| --accent-red | #c41e3a | Birincil vurgu (az ve keskin kullan) |
| --accent-silver | #c0c0c0 | İkincil vurgu, metin |
| Font display | Syne 800 | Başlıklar |
| Font mono | JetBrains Mono | Metin, kod, etiketler |

Kurallar:
- Border-radius: 0 veya max 2px — yuvarlak hiçbir şey yok
- Inter, Roboto, Arial gibi generic fontlar YASAK
- "Hoşgeldiniz", "Hakkımda" gibi amatör başlıklar YASAK
- Genel his: Askeri istihbarat raporu, terminal estetiği, sessiz otorite

## Dosya Yapısı
tahatokgoz.com/
├── index.html                    # Ana portfolyo sayfası
├── chain-sentinel.html           # Chain Sentinel proje detay sayfası
├── sitemap.xml                   # SEO site haritası (yeni sayfa eklenince güncelle)
├── robots.txt                    # Tarayıcı kuralları
├── CNAME                        # GitHub Pages custom domain (SİLME)
├── CLAUDE.md                    # Bu dosya
└── assets/
├── chain-sentinel/
│   ├── dashboard.png
│   ├── findings.png          # ⚠️ IP adresleri karalanmış, dosya adını koru
│   ├── ai-settings.png
│   ├── ai-analysis.png
│   └── mitre-mapping.png
└── publications/
└── imisc-2025-paper.pdf  # IMISC 2025 bildiri (88. sayfa)

## İçerik Modeli (index.html)
Portfolyo bölümleri DATA-DRIVEN. ~880. satırda 5 veri yapısı var:

| Array / Object | Section | Render Fonksiyonu |
|---|---|---|
| `projects` | #opsGrid — Active Operations | `renderOperations()` |
| `experiences` | #expGrid — Field Experience | `renderExperience()` |
| `arsenal` | #arsenalGrid — Technical Arsenal | `renderArsenal()` |
| `publications` | #pubGrid — Intelligence Reports | `renderPublications()` |
| `comms` | #commsBlock — Secure Comms | `renderComms()` |

İçerik eklemek/düzenlemek için SADECE array'i değiştir — HTML'e elle kart yazma.
Her array'in üstünde Türkçe yorum satırı var: `// YENİ PROJE EKLEMEK İÇİN BU ARRAY'E OBJE EKLE`
Boş array → ilgili section otomatik gizlenir.
`link` alanı doluysa kart tıklanabilir olur (örn: Chain Sentinel → chain-sentinel.html).

⚠️ Array'lerdeki string'ler innerHTML ile DOM'a enjekte edilir — güvenilir yazar içeriği olarak kabul edilir.

## Güvenlik Kuralları
- Yüklenen görsellerde hassas veri kontrolü YAP (IP adresi, API key, şifre, token, email, path bilgisi)
- Hassas veri varsa UYAR, yükleme yapma
- Görselde IP karalama gerekiyorsa opak (katı siyah) çizgi kullan, blur/pixelate kullanma
- Screenshot dosya adlarını değiştirme — mevcut `<img>` referansları bozulur
- `CNAME` dosyasını silme veya değiştirme

## Yeni Sayfa Ekleme Prosedürü
1. Mevcut sayfayı (chain-sentinel.html) şablon olarak kopyala
2. Aynı tasarım DNA'sını koru (Three.js, GSAP, Lenis, renk paleti, fontlar)
3. `index.html`'deki ilgili projects array'ine `link` alanı ekle
4. `sitemap.xml`'e yeni URL ekle ve `lastmod` tarihini güncelle
5. SEO meta taglarını (title, description, og:title, canonical) yeni sayfaya göre ayarla
6. Mobile responsive test yap (en küçük: 375px)
7. Commit ve push: `git add . && git commit -m "mesaj" && git push`

## Planlanan Sayfalar (Henüz Yapılmadı)
- `ti-bot.html` — TI-Bot proje detay sayfası (screenshot'lar hazır olunca)
- `pyscan.html` — pyscan proje detay sayfası (screenshot'lar hazır olunca)

Her ikisi de terminal mockup (HTML/CSS ile gerçekçi terminal penceresi) içerecek.

## Deploy
```bash
cd C:\Users\Taha\Projects\tahatokgoz.com
git add .
git commit -m "açıklayıcı mesaj"
git push
```
GitHub Pages 1-2 dakika içinde otomatik günceller.
Hard refresh: Ctrl+Shift+R (eski cache'i temizler)

## Local Preview
```bash
cd C:\Users\Taha\Projects\tahatokgoz.com
npx serve . -l 3000
# veya
python -m http.server 8000
```

## SEO
- Google Search Console doğrulanmış (DNS TXT kaydı ile)
- sitemap.xml gönderilmiş
- Dizine ekleme isteği yapılmış
- Yeni sayfa eklendiğinde sitemap.xml güncelle ve Search Console'dan tekrar indexleme iste

## Sistem Bilgisi
- OS: Windows 11 Pro
- Terminal: PowerShell
- Git: Kurulu, global config ayarlı (taha@tahatokgoz.com)
- Node.js: v24.14.1 (npx serve için)
- Repo: github.com/tahatokgoz/tahatokgoz.com (public, main branch)