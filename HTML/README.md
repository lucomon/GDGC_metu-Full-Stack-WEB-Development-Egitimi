# 📚 HTML Eğitimi

Bu doküman, HTML öğrenmek isteyenler için başlangıç seviyesinden orta seviyeye kadar bir eğitim rehberidir.  
HTML (*HyperText Markup Language*), web sayfalarının iskeletini oluşturan işaretleme dilidir.

---

## 🎯 İçindekiler
1. [HTML Nedir?](#-html-nedir)
2. [Temel HTML Yapısı](#-temel-html-yapısı)
3. [Başlıklar ve Paragraflar](#-başlıklar-ve-paragraflar)
4. [Metin Biçimlendirme](#-metin-biçimlendirme)
5. [Bağlantılar (Links)](#-bağlantılar-links)
6. [Görseller (Images)](#-görseller-images)
7. [Listeler](#-listeler)
8. [Tablolar](#-tablolar)
9. [Formlar](#-formlar)
10. [Semantic HTML](#-semantic-html)
11. [Kaynaklar](#-kaynaklar)

---

## 📌 HTML Nedir?
- HTML, web sayfalarının temel yapısını tanımlar.
- CSS ile görsel stil, JavaScript ile etkileşim eklenir.
- Bir HTML dosyasının uzantısı `.html` veya `.htm` olur.

---

## 🏗 Temel HTML Yapısı

```html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Merhaba HTML</title>
</head>
<body>
    <h1>Merhaba Dünya!</h1>
    <p>Bu benim ilk HTML sayfam.</p>
</body>
</html>
```

- **`<!DOCTYPE html>`** → HTML5 standardını belirtir.
- **`<html>`** → Sayfanın tüm içeriğini kapsar.
- **`<head>`** → Başlık, meta bilgileri, CSS ve JS dosyaları eklenir.
- **`<body>`** → Kullanıcıya görünen içerik.

---

## 📝 Başlıklar ve Paragraflar

```html
<h1>Başlık 1</h1>
<h2>Başlık 2</h2>
<h3>Başlık 3</h3>
<p>Bu bir paragraf örneğidir.</p>
```

- **`<h1>`** en büyük başlıktır, **`<h6>`** en küçüğüdür.
- **`<p>`** paragraf metinleri için kullanılır.

---

## ✏ Metin Biçimlendirme

```html
<p><b>Kalın metin</b> ve <i>italik metin</i>.</p>
<p><strong>Önemli metin</strong> ve <em>vurgulu metin</em>.</p>
<p><u>Altı çizili</u> ve <mark>vurgulanmış</mark> metin.</p>
```

---

## 🔗 Bağlantılar (Links)

```html
<a href="https://www.google.com" target="_blank">Google'a git</a>
```

- **`href`** → Hedef URL.
- **`target="_blank"`** → Yeni sekmede açar.

---

## 🖼 Görseller (Images)

```html
<img src="resim.jpg" alt="Açıklama" width="300">
```

- **`src`** → Resmin yolu.
- **`alt`** → Erişilebilirlik açıklaması.
- **`width`** / **`height`** → Boyut.

---

## 📋 Listeler

**Sırasız Liste**
```html
<ul>
    <li>Elma</li>
    <li>Armut</li>
    <li>Muz</li>
</ul>
```

**Sıralı Liste**
```html
<ol>
    <li>Adım 1</li>
    <li>Adım 2</li>
    <li>Adım 3</li>
</ol>
```

---

## 📊 Tablolar

```html
<table border="1">
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

## 📮 Formlar

```html
<form action="/gonder" method="POST">
    <label>Adınız:</label>
    <input type="text" name="ad" required>
    
    <label>E-posta:</label>
    <input type="email" name="email" required>
    
    <input type="submit" value="Gönder">
</form>
```

---

## 🏷 Semantic HTML
Semantic (anlamlı) etiketler, içeriğin amacını belirtir:
- `<header>` → Üst bölüm
- `<nav>` → Menü
- `<main>` → Ana içerik
- `<section>` → Bölüm
- `<article>` → Makale
- `<footer>` → Alt bilgi

---

