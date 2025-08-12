# 📚 HTML Eğitimi - Detaylı Rehber

Bu doküman, HTML öğrenmek isteyenler için **başlangıç seviyesinden ileri seviyeye** kadar kapsamlı bir eğitim rehberidir.  
HTML (*HyperText Markup Language*), web sayfalarının iskeletini oluşturan **işaretleme dilidir**. CSS ile görünüm, JavaScript ile etkileşim eklenir.

---

## 🎯 İçindekiler
1. [HTML Nedir?](#-html-nedir)
2. [HTML Kurulumu ve İlk Sayfa](#-html-kurulumu-ve-ilk-sayfa)
3. [HTML Temel Yapısı](#-html-temel-yapısı)
4. [Başlıklar ve Paragraflar](#-başlıklar-ve-paragraflar)
5. [Metin Biçimlendirme Etiketleri](#-metin-biçimlendirme-etiketleri)
6. [Bağlantılar (Links)](#-bağlantılar-links)
7. [Görseller (Images)](#-görseller-images)
8. [Listeler (Lists)](#-listeler-lists)
9. [Tablolar (Tables)](#-tablolar-tables)
10. [Formlar ve Giriş Elemanları](#-formlar-ve-giriş-elemanları)
11. [Multimedya Etiketleri](#-multimedya-etiketleri)
12. [Semantic HTML](#-semantic-html)
13. [Meta Etiketler ve SEO](#-meta-etiketler-ve-seo)
14. [HTML5 Yenilikleri](#-html5-yenilikleri)
15. [En İyi Uygulamalar](#-en-iyi-uygulamalar)
16. [Kaynaklar](#-kaynaklar)

---

## 📌 HTML Nedir?
- **HTML**, web sayfalarının temel yapısını tanımlayan bir işaretleme dilidir.
- 1991 yılında **Tim Berners-Lee** tarafından geliştirilmiştir.
- **HTML** tek başına görsel stil veya etkileşim sağlamaz, bu iş için **CSS** ve **JavaScript** kullanılır.

---

## 🖥 HTML Kurulumu ve İlk Sayfa

HTML kodlarını çalıştırmak için yalnızca bir **metin editörü** ve **web tarayıcısı** yeterlidir.

**Adımlar:**
1. Masaüstünde `index.html` isminde bir dosya oluşturun.
2. Aşağıdaki kodları yapıştırın:
```html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>İlk HTML Sayfam</title>
</head>
<body>
    <h1>Merhaba Dünya!</h1>
    <p>Bu benim ilk HTML sayfam.</p>
</body>
</html>
```
3. Dosyayı kaydedin ve çift tıklayarak tarayıcıda açın.

---

## 🏗 HTML Temel Yapısı

Bir HTML belgesi şu ana bölümlerden oluşur:

| Bölüm | Açıklama |
|-------|----------|
| `<!DOCTYPE html>` | HTML5 kullanıldığını belirtir |
| `<html>` | Sayfanın tamamını kapsar |
| `<head>` | Meta bilgiler, başlık, stil dosyaları |
| `<body>` | Görünecek içerikler |

---

## 📝 Başlıklar ve Paragraflar

```html
<h1>Başlık 1</h1>
<h2>Başlık 2</h2>
<h3>Başlık 3</h3>
<p>Bu bir paragraf örneğidir.</p>
```

**Not:** Bir sayfada **sadece bir tane `<h1>`** kullanılması SEO açısından daha iyidir.

---

## ✏ Metin Biçimlendirme Etiketleri

| Etiket | Açıklama |
|--------|----------|
| `<b>` | Kalın metin |
| `<strong>` | Önemli metin (SEO etkili) |
| `<i>` | İtalik metin |
| `<em>` | Vurgulu metin |
| `<u>` | Altı çizili metin |
| `<mark>` | Arka planı vurgulu metin |

**Örnek:**
```html
<p><strong>Önemli</strong> kelimeyi <em>vurgulamak</em> için kullanılır.</p>
```

---

## 🔗 Bağlantılar (Links)

```html
<a href="https://www.google.com" target="_blank">Google</a>
```

**Özellikler:**
- `href` → Bağlantı adresi
- `target="_blank"` → Yeni sekmede açar
- `title` → Üzerine gelince görünen bilgi

---

## 🖼 Görseller (Images)

```html
<img src="resim.jpg" alt="Açıklama" width="300">
```

- `src` → Resim yolu
- `alt` → Erişilebilirlik için açıklama
- `width` ve `height` → Boyut

---

## 📋 Listeler (Lists)

**Sırasız Liste**
```html
<ul>
    <li>Elma</li>
    <li>Armut</li>
</ul>
```

**Sıralı Liste**
```html
<ol>
    <li>Adım 1</li>
    <li>Adım 2</li>
</ol>
```

**Tanım Listesi**
```html
<dl>
    <dt>HTML</dt>
    <dd>Web sayfa iskeletini oluşturur</dd>
</dl>
```

---

## 📊 Tablolar (Tables)

```html
<table border="1">
    <caption>Öğrenci Listesi</caption>
    <tr>
        <th>Ad</th>
        <th>Yaş</th>
    </tr>
    <tr>
        <td>Ali</td>
        <td>25</td>
    </tr>
</table>
```

---

## 📮 Formlar ve Giriş Elemanları

```html
<form action="/gonder" method="POST">
    <label>Adınız:</label>
    <input type="text" name="ad" required>
    
    <label>E-posta:</label>
    <input type="email" name="email" required>
    
    <label>Mesaj:</label>
    <textarea name="mesaj"></textarea>

    <input type="submit" value="Gönder">
</form>
```

---

## 🎵🎥 Multimedya Etiketleri

```html
<audio controls>
    <source src="ses.mp3" type="audio/mpeg">
</audio>

<video controls width="400">
    <source src="video.mp4" type="video/mp4">
</video>
```

---

## 🏷 Semantic HTML

| Etiket | Kullanım |
|--------|----------|
| `<header>` | Üst kısım |
| `<nav>` | Menü |
| `<main>` | Ana içerik |
| `<section>` | Bölüm |
| `<article>` | Makale |
| `<footer>` | Alt bilgi |

---

## 🌐 Meta Etiketler ve SEO

```html
<meta name="description" content="HTML eğitim rehberi">
<meta name="keywords" content="HTML, eğitim, web geliştirme">
<meta name="author" content="Senin Adın">
```

---

## 🚀 HTML5 Yenilikleri
- `<video>` ve `<audio>` desteği
- `<canvas>` ile çizim
- `<section>`, `<article>` gibi anlamlı etiketler
- Form giriş tipleri (`email`, `date`, `range`)

---

## ✅ En İyi Uygulamalar
- Etiketleri kapatmayı unutmayın.
- Anlamlı etiketler kullanın.
- Resimlerde mutlaka `alt` ekleyin.
- Kodunuzu düzenli girintileyin.

---

