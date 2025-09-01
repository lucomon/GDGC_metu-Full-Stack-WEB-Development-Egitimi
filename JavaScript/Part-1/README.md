# JavaScript Temelleri - Eğitim Materyali

## 📚 İçindekiler
- [JavaScript Nedir?](#javascript-nedir)
- [JavaScript Çalıştırma](#javascript-çalıştırma)
- [Kod Yorumları](#kod-yorumları)
- [Değişkenler](#değişkenler)
- [Operatörler](#operatörler)
- [Matematik İşlemleri](#matematik-işlemleri)
- [String (Metin) İşlemleri](#string-metin-işlemleri)
- [Diziler (Arrays)](#diziler-arrays)
- [Fonksiyonlar](#fonksiyonlar)
- [Kapsam (Scope)](#kapsam-scope)
- [Koşul İfadeleri](#koşul-ifadeleri)
- [Switch Statements](#switch-statements)
- [Pratik Örnekler](#pratik-örnekler)
- [Ödevler](#ödevler)

---

## 🌐 JavaScript Nedir?

**JavaScript**, web sayfalarını etkileşimli hale getirmek için kullanılan programlama dilidir. HTML yapıyı, CSS görünümü oluştururken, JavaScript bu yapıya dinamik davranış ekler.

### JavaScript'in Temel Özellikleri:
- **Dinamik** - Sayfa yüklendikten sonra değişiklik yapabilir
- **Etkileşimli** - Kullanıcı girişlerine tepki verebilir
- **Çok yönlü** - Frontend ve backend'de kullanılabilir
- **Modern** - Güncel web teknolojilerinin temelidir

---

## 🚀 JavaScript Çalıştırma

### Tarayıcıda Çalıştırma
JavaScript kodunu tarayıcıda çalıştırmak için birkaç yöntem vardır:

#### 1. HTML Dosyasında
```html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JavaScript Örneği</title>
</head>
<body>
    <h1>JavaScript Test</h1>
    
    <!-- JavaScript kodunu buraya yazabilirsiniz -->
    <script>
        console.log("Merhaba JavaScript!");
        alert("JavaScript çalışıyor!");
    </script>
</body>
</html>
```

#### 2. Harici JavaScript Dosyası
```html
<head>
    <script src="script.js"></script>
</head>
```

#### 3. Tarayıcı Konsolunda
- F12 tuşuna basın
- Console sekmesine gidin
- JavaScript kodunu yazın ve Enter'a basın

### Node.js ile Çalıştırma
```bash
# JavaScript dosyasını çalıştırma
node dosyaadi.js

# Node.js REPL (Interactive mode)
node
```

---

## 💬 Kod Yorumları

Kod yorumları, kodunuzu açıklamak ve diğer geliştiricilerin anlamasını kolaylaştırmak için kullanılır.

### Tek Satır Yorumları
```javascript
// Bu bir tek satır yorumudur
let isim = "Faruk"; // Değişken tanımlama
```

### Çok Satır Yorumları
```javascript
/*
Bu bir çok satır yorumudur
Birden fazla satır yazabilirsiniz
Kodunuzu açıklamak için kullanın
*/
```

### Yorum Kullanım Örnekleri
```javascript
// Kullanıcı adını al
let kullaniciAdi = prompt("Adınız nedir?");

// Yaş hesaplama
let dogumYili = 1990;
let guncelYil = 2024;
let yas = guncelYil - dogumYili;

/*
Bu fonksiyon kullanıcının yaşını hesaplar
Parametre olarak doğum yılını alır
Güncel yıldan çıkararak yaşı döndürür
*/
function yasHesapla(dogumYili) {
    return 2024 - dogumYili;
}
```

---

## 📊 Temel Veri Tipleri

JavaScript'te veriler farklı türlerde olabilir. Her veri tipinin kendine özgü özellikleri ve davranışları vardır.

### Primitive (İlkel) Veri Tipleri

#### 1. String (Metin)
```javascript
let isim = "Faruk";
let soyad = 'Güvenkaya';
let mesaj = `Merhaba ${isim}!`; // Template literal

console.log(typeof isim); // "string"
```

#### 2. Number (Sayı)
JavaScript'te tüm sayılar `number` tipindedir. JavaScript, integer (tam sayı) ve float (ondalıklı sayı) arasında ayrım yapmaz.

```javascript
// Integer (Tam Sayılar)
let tamSayi = 42;
let negatifTam = -10;
let sifir = 0;
let buyukSayi = 1000000;

// Float (Ondalıklı Sayılar)
let ondalik = 3.14;
let negatifOndalik = -2.5;
let bilimsel = 1.23e-4; // 0.000123
let buyukOndalik = 1.23e+6; // 1230000

// Özel Number Değerleri
let sonsuz = Infinity;
let negatifSonsuz = -Infinity;
let sayiDegil = NaN; // Not a Number

console.log(typeof tamSayi); // "number"
console.log(typeof ondalik); // "number"
console.log(typeof bilimsel); // "number"
```

##### Number Sınırları ve Hassasiyet
```javascript
// JavaScript'te Number sınırları
console.log(Number.MAX_VALUE);     // 1.7976931348623157e+308
console.log(Number.MIN_VALUE);     // 5e-324
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
console.log(Number.MIN_SAFE_INTEGER); // -9007199254740991

// Hassasiyet sorunları (Float hesaplamalarında)
let a = 0.1;
let b = 0.2;
console.log(a + b); // 0.30000000000000004 (Beklenen: 0.3)

// Çözüm: Math.round() veya toFixed()
console.log(Math.round((a + b) * 100) / 100); // 0.3
console.log((a + b).toFixed(2)); // "0.30"
```

##### Number Metodları
```javascript
let sayi = 3.14159;

// Yuvarlama metodları
console.log(Math.round(sayi));    // 3 (En yakın tam sayıya)
console.log(Math.floor(sayi));    // 3 (Aşağı yuvarlama)
console.log(Math.ceil(sayi));     // 4 (Yukarı yuvarlama)
console.log(Math.trunc(sayi));    // 3 (Ondalık kısmı atma)

// Mutlak değer
console.log(Math.abs(-42));       // 42

// Üs alma
console.log(Math.pow(2, 3));      // 8
console.log(2 ** 3);              // 8 (ES6 üs operatörü)

// Karekök
console.log(Math.sqrt(16));       // 4

// Rastgele sayı (0-1 arası)
console.log(Math.random());       // 0.123456789...
console.log(Math.floor(Math.random() * 100)); // 0-99 arası tam sayı
```

#### 3. Boolean (Mantıksal)
```javascript
let dogru = true;
let yanlis = false;

console.log(typeof dogru); // "boolean"
```

#### 4. Undefined (Tanımsız)
```javascript
let tanimsiz;
console.log(tanimsiz); // undefined
console.log(typeof tanimsiz); // "undefined"
```

#### 5. Null (Boş)
```javascript
let bos = null;
console.log(bos); // null
console.log(typeof bos); // "object" (JavaScript'te bilinen bir hata)
```

#### 6. Symbol (Sembol) - ES6
```javascript
let sembol = Symbol("açıklama");
console.log(typeof sembol); // "symbol"
```

### Reference (Referans) Veri Tipleri

#### 7. Object (Nesne)
```javascript
let kullanici = {
    isim: "Faruk",
    yas: 25,
    aktif: true
};

console.log(typeof kullanici); // "object"
```

#### 8. Array (Dizi)
```javascript
let renkler = ["kırmızı", "mavi", "yeşil"];
let sayilar = [1, 2, 3, 4, 5];

console.log(typeof renkler); // "object" (diziler de objedir)
console.log(Array.isArray(renkler)); // true (dizi kontrolü)
```

#### 9. Function (Fonksiyon)
```javascript
function selamla() {
    return "Merhaba!";
}

console.log(typeof selamla); // "function"
```

### Veri Tipi Kontrolü
```javascript
// typeof operatörü ile tip kontrolü
let metin = "Merhaba";
let sayi = 42;
let mantik = true;

console.log(typeof metin);   // "string"
console.log(typeof sayi);    // "number"
console.log(typeof mantik);  // "boolean"

// Array kontrolü
let dizi = [1, 2, 3];
console.log(Array.isArray(dizi)); // true
console.log(typeof dizi);         // "object"
```

### Veri Tipi Dönüşümleri
```javascript
// String'e dönüştürme
let sayi = 42;
let metin = String(sayi);        // "42"
let metin2 = sayi.toString();    // "42"

// Number'a dönüştürme
let metin = "42";
let sayi = Number(metin);        // 42
let sayi2 = parseInt(metin);     // 42
let sayi3 = parseFloat("3.14");  // 3.14

// Boolean'a dönüştürme
let metin = "Merhaba";
let mantik = Boolean(metin);     // true
let mantik2 = !!metin;           // true (çift ünlem ile)
```

---

## 📦 Değişkenler

Değişkenler, veri saklamak için kullanılan konteynerlerdir.

### Değişken Tanımlama

#### 1. `let` ile Tanımlama (Önerilen)
```javascript
let isim = "Faruk";
let yas = 25;
let aktifMi = true;

// Değer değiştirilebilir
yas = 26;
console.log(yas); // 26
```

#### 2. `const` ile Tanımlama (Sabit Değerler)
```javascript
const PI = 3.14159;
const UYGULAMA_ADI = "Web Eğitim";

// const ile tanımlanan değişkenler değiştirilemez
// PI = 3.14; // Hata verir!
```

#### 3. `var` ile Tanımlama (Eski Yöntem)
```javascript
var eskiDegisken = "Eski yöntem";
// Modern JavaScript'te let kullanın
```

### Değişken İsimlendirme Kuralları
```javascript
// Doğru isimlendirmeler
let kullaniciAdi = "Faruk";
let kullanici_yasi = 25;
let kullaniciYasi = 25;

// Yanlış isimlendirmeler
// let 1isim = "Faruk";     // Sayı ile başlayamaz
// let isim-soyisim = "Faruk"; // Tire kullanılamaz
// let let = "kelime";      // JavaScript anahtar kelimesi olamaz
```

### Değişken Türleri
```javascript
// String (Metin)
let isim = "Faruk Bora Güvenkaya";
let mesaj = 'Merhaba Dünya';

// Number (Sayı)
let yas = 25;
let boy = 1.75;
let negatif = -10;

// Boolean (Mantıksal)
let aktif = true;
let pasif = false;

// Undefined (Tanımsız)
let tanimsiz;

// Null (Boş)
let bos = null;

// Object (Nesne)
let kullanici = {
    isim: "Faruk",
    yas: 25
};

// Array (Dizi)
let renkler = ["kırmızı", "mavi", "yeşil"];
```

---

## 🔧 Operatörler

### Atama Operatörü
```javascript
// Basit atama
let x = 5;

// Toplama ile atama
x += 3; // x = x + 3 ile aynı
console.log(x); // 8

// Çıkarma ile atama
x -= 2; // x = x - 2 ile aynı
console.log(x); // 6

// Çarpma ile atama
x *= 4; // x = x * 4 ile aynı
console.log(x); // 24

// Bölme ile atama
x /= 3; // x = x / 3 ile aynı
console.log(x); // 8
```

### Karşılaştırma Operatörleri
```javascript
let a = 5;
let b = 10;

// Eşitlik
console.log(a == 5);   // true (değer karşılaştırması)
console.log(a === 5);  // true (değer ve tip karşılaştırması)
console.log(a == "5"); // true (tip dönüşümü ile)
console.log(a === "5"); // false (tip farklı)

// Eşitsizlik
console.log(a != 10);  // true
console.log(a !== "5"); // true

// Büyük/küçük
console.log(a < b);    // true
console.log(a > b);    // false
console.log(a <= 5);   // true
console.log(a >= 5);   // true
```

### Mantıksal Operatörler
```javascript
let yas = 25;
let para = 1000;

// AND (VE) operatörü
if (yas >= 18 && para >= 500) {
    console.log("Alışveriş yapabilirsiniz");
}

// OR (VEYA) operatörü
if (yas < 18 || para < 100) {
    console.log("İndirim alabilirsiniz");
}

// NOT (DEĞİL) operatörü
if (!(yas < 18)) {
    console.log("Yetişkinsiniz");
}
```

---

## ➕ Matematik İşlemleri

### Temel Matematik Operatörleri
```javascript
let a = 10;
let b = 3;

// Toplama
let toplam = a + b;        // 13
console.log("Toplam:", toplam);

// Çıkarma
let fark = a - b;          // 7
console.log("Fark:", fark);

// Çarpma
let carpim = a * b;        // 30
console.log("Çarpım:", carpim);

// Bölme
let bolum = a / b;         // 3.333...
console.log("Bölüm:", bolum);

// Mod (Kalan)
let kalan = a % b;         // 1
console.log("Kalan:", kalan);

// Üs alma
let us = a ** b;           // 1000
console.log("Üs:", us);
```

### Artırma ve Azaltma
```javascript
let sayi = 5;

// Önce artır, sonra kullan
console.log(++sayi);       // 6 (sayi = 6)

// Önce kullan, sonra artır
console.log(sayi++);       // 6 (sayi = 7)

// Önce azalt, sonra kullan
console.log(--sayi);       // 6 (sayi = 6)

// Önce kullan, sonra azalt
console.log(sayi--);       // 6 (sayi = 5)

console.log("Son değer:", sayi); // 5
```

### Ondalıklı Sayılar
```javascript
let ondalik1 = 3.14;
let ondalik2 = 2.5;

// Çarpma
let carpim = ondalik1 * ondalik2;  // 7.85
console.log("Çarpım:", carpim);

// Bölme
let bolum = ondalik1 / ondalik2;   // 1.256
console.log("Bölüm:", bolum);

// Toplama
let toplam = ondalik1 + ondalik2;  // 5.64
console.log("Toplam:", toplam);

// Çıkarma
let fark = ondalik1 - ondalik2;    // 0.64
console.log("Fark:", fark);
```

### Matematik İşlemleri Örnekleri
```javascript
// Daire alanı hesaplama
let yaricap = 5;
let pi = 3.14159;
let alan = pi * yaricap * yaricap;
console.log("Daire alanı:", alan);

// Ortalama hesaplama
let not1 = 85;
let not2 = 90;
let not3 = 78;
let ortalama = (not1 + not2 + not3) / 3;
console.log("Not ortalaması:", ortalama);

// Yüzde hesaplama
let fiyat = 100;
let indirim = 20;
let indirimliFiyat = fiyat - (fiyat * indirim / 100);
console.log("İndirimli fiyat:", indirimliFiyat);
```

---

## 📝 String (Metin) İşlemleri

### String Tanımlama
```javascript
// Çift tırnak
let isim1 = "Faruk";

// Tek tırnak
let isim2 = 'Bora';

// Backtick (Template literal)
let isim3 = `Güvenkaya`;

// Değişken ile string oluşturma
let tamIsim = isim1 + " " + isim2 + " " + isim3;
console.log(tamIsim); // "Faruk Bora Güvenkaya"
```

### String Birleştirme
```javascript
let ad = "Faruk";
let soyad = "Güvenkaya";

// + operatörü ile
let tamAd = ad + " " + soyad;
console.log(tamAd); // "Faruk Güvenkaya"

// += operatörü ile
let mesaj = "Merhaba ";
mesaj += ad;
console.log(mesaj); // "Merhaba Faruk"

// Template literal ile
let selamlama = `Merhaba ${ad} ${soyad}!`;
console.log(selamlama); // "Merhaba Faruk Güvenkaya!"
```

### String Özellikleri ve Metodları
```javascript
let metin = "JavaScript Öğreniyorum";

// Uzunluk
console.log(metin.length); // 23

// Belirli karaktere erişim
console.log(metin[0]);     // "J"
console.log(metin[5]);     // "c"

// Büyük/küçük harf
console.log(metin.toUpperCase()); // "JAVASCRIPT ÖĞRENİYORUM"
console.log(metin.toLowerCase()); // "javascript öğreniyorum"

// Karakter arama
console.log(metin.indexOf("Ö"));     // 12
console.log(metin.includes("Java")); // true

// Parça alma
console.log(metin.substring(0, 10)); // "JavaScript"
console.log(metin.slice(-10));       // "öğreniyorum"
```

### Escape Sequences (Kaçış Dizileri)
```javascript
// Yeni satır
let cokSatirli = "Satır 1\nSatır 2";
console.log(cokSatirli);

// Tab
let tabli = "Ad\tSoyad\tYaş";
console.log(tabli);

// Tırnak işaretleri
let tirnakli = "O \"JavaScript\" öğreniyor";
let tekTirnakli = 'O \'JavaScript\' öğreniyor';
console.log(tirnakli);
console.log(tekTirnakli);

// Backslash
let backslash = "C:\\Users\\Faruk\\Desktop";
console.log(backslash);
```

### String Örnekleri
```javascript
// Kullanıcı bilgilerini birleştirme
let ad = "Faruk";
let soyad = "Güvenkaya";
let yas = 25;
let meslek = "Web Geliştirici";

let profil = `
Kullanıcı Profili:
Ad: ${ad}
Soyad: ${soyad}
Yaş: ${yas}
Meslek: ${meslek}
`;

console.log(profil);

// Kelime sayısı hesaplama
let cumle = "JavaScript öğrenmek çok eğlenceli";
let kelimeSayisi = cumle.split(" ").length;
console.log("Kelime sayısı:", kelimeSayisi);

// Palindrom kontrolü
function palindromKontrol(metin) {
    let temizMetin = metin.toLowerCase().replace(/[^a-z0-9]/g, "");
    let tersMetin = temizMetin.split("").reverse().join("");
    return temizMetin === tersMetin;
}

console.log(palindromKontrol("Eve")); // true
console.log(palindromKontrol("Merhaba")); // false
```

---

## 📊 Diziler (Arrays)

### Dizi Oluşturma
```javascript
// Boş dizi
let bosDizi = [];

// Elemanlı dizi
let renkler = ["kırmızı", "mavi", "yeşil"];
let sayilar = [1, 2, 3, 4, 5];
let karisik = ["metin", 42, true, null];

// Dizi uzunluğu
console.log(renkler.length); // 3
```

### Dizi Elemanlarına Erişim
```javascript
let meyveler = ["elma", "armut", "muz", "portakal"];

// İndeks ile erişim (0'dan başlar)
console.log(meyveler[0]); // "elma"
console.log(meyveler[2]); // "muz"
console.log(meyveler[meyveler.length - 1]); // "portakal" (son eleman)
```

### Dizi Elemanlarını Değiştirme
```javascript
let renkler = ["kırmızı", "mavi", "yeşil"];

// Belirli indeksteki elemanı değiştir
renkler[1] = "sarı";
console.log(renkler); // ["kırmızı", "sarı", "yeşil"]

// Diziye yeni eleman ekle
renkler[3] = "mor";
console.log(renkler); // ["kırmızı", "sarı", "yeşil", "mor"]
```

### Dizi Metodları
```javascript
let alisverisListesi = ["ekmek", "süt"];

// push() - Sona eleman ekleme
alisverisListesi.push("yumurta");
console.log(alisverisListesi); // ["ekmek", "süt", "yumurta"]

// pop() - Sondan eleman çıkarma
let sonEleman = alisverisListesi.pop();
console.log(sonEleman); // "yumurta"
console.log(alisverisListesi); // ["ekmek", "süt"]

// unshift() - Başa eleman ekleme
alisverisListesi.unshift("domates");
console.log(alisverisListesi); // ["domates", "ekmek", "süt"]

// shift() - Baştan eleman çıkarma
let ilkEleman = alisverisListesi.shift();
console.log(ilkEleman); // "domates"
console.log(alisverisListesi); // ["ekmek", "süt"]
```

### İç İçe Diziler (Nested Arrays)
```javascript
// 2 boyutlu dizi (matris)
let matris = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

// Elemana erişim
console.log(matris[0][1]); // 2
console.log(matris[2][2]); // 9

// 3 boyutlu dizi
let kutu = [
    [
        ["a", "b"],
        ["c", "d"]
    ],
    [
        ["e", "f"],
        ["g", "h"]
    ]
];

console.log(kutu[0][1][0]); // "c"
```

### Dizi Örnekleri
```javascript
// Alışveriş listesi uygulaması
let alisverisListesi = [];

function urunEkle(urun) {
    alisverisListesi.push(urun);
    console.log(`${urun} listeye eklendi.`);
}

function urunCikar(urun) {
    let index = alisverisListesi.indexOf(urun);
    if (index > -1) {
        alisverisListesi.splice(index, 1);
        console.log(`${urun} listeden çıkarıldı.`);
    } else {
        console.log(`${urun} listede bulunamadı.`);
    }
}

function listeyiGoster() {
    if (alisverisListesi.length === 0) {
        console.log("Alışveriş listesi boş.");
    } else {
        console.log("Alışveriş Listesi:");
        alisverisListesi.forEach((urun, index) => {
            console.log(`${index + 1}. ${urun}`);
        });
    }
}

// Test
urunEkle("ekmek");
urunEkle("süt");
urunEkle("yumurta");
listeyiGoster();
urunCikar("süt");
listeyiGoster();
```

---

## ⚙️ Fonksiyonlar

### Fonksiyon Tanımlama
```javascript
// Fonksiyon tanımlama
function selamla() {
    console.log("Merhaba!");
}

// Fonksiyonu çağırma
selamla(); // "Merhaba!" yazdırır

// Parametreli fonksiyon
function selamlaKullanici(isim) {
    console.log(`Merhaba ${isim}!`);
}

selamlaKullanici("Faruk"); // "Merhaba Faruk!" yazdırır
```

### Fonksiyon Parametreleri
```javascript
// Tek parametre
function kareAl(sayi) {
    return sayi * sayi;
}

console.log(kareAl(5)); // 25

// Birden fazla parametre
function topla(a, b) {
    return a + b;
}

console.log(topla(10, 20)); // 30

// Varsayılan parametre
function selamla(isim = "Misafir") {
    console.log(`Merhaba ${isim}!`);
}

selamla(); // "Merhaba Misafir!"
selamla("Faruk"); // "Merhaba Faruk!"
```

### Return Değeri
```javascript
// Değer döndüren fonksiyon
function yasHesapla(dogumYili) {
    let yas = 2024 - dogumYili;
    return yas;
}

let yas = yasHesapla(1990);
console.log("Yaşınız:", yas); // 34

// Return olmayan fonksiyon
function selamla() {
    console.log("Merhaba!");
    // return yok, undefined döner
}

let sonuc = selamla();
console.log(sonuc); // undefined
```

### Fonksiyon Örnekleri
```javascript
// Hesap makinesi fonksiyonları
function topla(a, b) {
    return a + b;
}

function cikar(a, b) {
    return a - b;
}

function carp(a, b) {
    return a * b;
}

function bol(a, b) {
    if (b === 0) {
        return "Sıfıra bölünemez!";
    }
    return a / b;
}

// Test
console.log("Toplam:", topla(10, 5));     // 15
console.log("Fark:", cikar(10, 5));       // 5
console.log("Çarpım:", carp(10, 5));      // 50
console.log("Bölüm:", bol(10, 5));        // 2
console.log("Bölüm:", bol(10, 0));        // "Sıfıra bölünemez!"

// Faktöriyel hesaplama
function faktoriyel(n) {
    if (n === 0 || n === 1) {
        return 1;
    }
    return n * faktoriyel(n - 1);
}

console.log("5! =", faktoriyel(5)); // 120
```

---

## 🌍 Kapsam (Scope)

### Global Kapsam
```javascript
// Global değişken
let globalDegisken = "Bu değişken her yerden erişilebilir";

function testFonksiyonu() {
    console.log(globalDegisken); // Global değişkene erişebilir
}

testFonksiyonu(); // "Bu değişken her yerden erişilebilir"
console.log(globalDegisken); // Global değişkene erişebilir
```

### Yerel Kapsam (Local Scope)
```javascript
function testFonksiyonu() {
    // Yerel değişken
    let yerelDegisken = "Bu değişken sadece fonksiyon içinde erişilebilir";
    console.log(yerelDegisken);
}

testFonksiyonu(); // "Bu değişken sadece fonksiyon içinde erişilebilir"

// console.log(yerelDegisken); // Hata! Değişken tanımlı değil
```

### Global vs Yerel Kapsam
```javascript
let isim = "Faruk"; // Global değişken

function testFonksiyonu() {
    let isim = "Bora"; // Yerel değişken (global'i gizler)
    console.log("Fonksiyon içinde:", isim); // "Bora"
}

testFonksiyonu();
console.log("Global:", isim); // "Faruk"

// Global değişkeni değiştirme
function isimDegistir() {
    isim = "Güvenkaya"; // Global değişkeni değiştirir
    console.log("Fonksiyon içinde:", isim); // "Güvenkaya"
}

isimDegistir();
console.log("Global:", isim); // "Güvenkaya"
```

### Kapsam Örnekleri
```javascript
// Sayaç örneği
let globalSayaç = 0;

function sayaciArtir() {
    let yerelSayaç = 0; // Her çağrıda sıfırlanır
    globalSayaç++;
    yerelSayaç++;
    
    console.log(`Global sayaç: ${globalSayaç}`);
    console.log(`Yerel sayaç: ${yerelSayaç}`);
}

sayaciArtir(); // Global: 1, Yerel: 1
sayaciArtir(); // Global: 2, Yerel: 1
sayaciArtir(); // Global: 3, Yerel: 1

// Block scope (let ile)
if (true) {
    let blockDegisken = "Block içinde";
    console.log(blockDegisken); // "Block içinde"
}
// console.log(blockDegisken); // Hata! Block dışında erişilemez
```

---

## 🔀 Koşul İfadeleri

### If Statements
```javascript
let yas = 18;

if (yas >= 18) {
    console.log("Yetişkinsiniz");
}

// Tek satır if
if (yas >= 18) console.log("Yetişkinsiniz");
```

### If-Else Statements
```javascript
let yas = 16;

if (yas >= 18) {
    console.log("Yetişkinsiniz");
} else {
    console.log("Reşit değilsiniz");
}
```

### Else-If Statements
```javascript
let not = 85;

if (not >= 90) {
    console.log("A");
} else if (not >= 80) {
    console.log("B");
} else if (not >= 70) {
    console.log("C");
} else if (not >= 60) {
    console.log("D");
} else {
    console.log("F");
}
```

### Boolean Values
```javascript
let dogru = true;
let yanlis = false;

if (dogru) {
    console.log("Bu çalışır");
}

if (!yanlis) {
    console.log("Bu da çalışır");
}

// Boolean dönüşümü
let yas = 18;
let yetiskinMi = yas >= 18; // true
console.log(yetiskinMi);
```

### Equality Operators
```javascript
let a = 5;
let b = "5";

// == (Eşitlik - tip dönüşümü ile)
console.log(a == b);   // true

// === (Strict equality - tip ve değer)
console.log(a === b);  // false

// != (Eşitsizlik)
console.log(a != b);   // false

// !== (Strict inequality)
console.log(a !== b);  // true
```

### Logical Operators
```javascript
let yas = 25;
let para = 1000;
let vakit = true;

// AND (VE) - Tüm koşullar doğru olmalı
if (yas >= 18 && para >= 500 && vakit) {
    console.log("Alışverişe gidebilirsiniz");
}

// OR (VEYA) - En az bir koşul doğru olmalı
if (yas < 18 || para < 100) {
    console.log("İndirim alabilirsiniz");
}

// NOT (DEĞİL) - Koşulu tersine çevirir
if (!(yas < 18)) {
    console.log("Yetişkinsiniz");
}
```

### Koşul Örnekleri
```javascript
// Not hesaplama sistemi
function notHesapla(puan) {
    if (puan >= 90) {
        return "A";
    } else if (puan >= 80) {
        return "B";
    } else if (puan >= 70) {
        return "C";
    } else if (puan >= 60) {
        return "D";
    } else {
        return "F";
    }
}

console.log(notHesapla(95)); // "A"
console.log(notHesapla(75)); // "C"
console.log(notHesapla(45)); // "F"

// Giriş kontrolü
function girisKontrol(kullaniciAdi, sifre) {
    if (kullaniciAdi === "admin" && sifre === "12345") {
        console.log("Giriş başarılı!");
        return true;
    } else {
        console.log("Kullanıcı adı veya şifre hatalı!");
        return false;
    }
}

girisKontrol("admin", "12345"); // Giriş başarılı!
girisKontrol("user", "password"); // Kullanıcı adı veya şifre hatalı!
```

---

## 🔀 Switch Statements

### Temel Switch Yapısı
```javascript
let gun = "pazartesi";

switch (gun) {
    case "pazartesi":
        console.log("Haftanın ilk günü");
        break;
    case "salı":
        console.log("Haftanın ikinci günü");
        break;
    case "çarşamba":
        console.log("Haftanın üçüncü günü");
        break;
    default:
        console.log("Diğer bir gün");
}
```

### Break Kullanımı
```javascript
let not = "B";

switch (not) {
    case "A":
        console.log("Mükemmel!");
        break;
    case "B":
        console.log("İyi!");
        break;
    case "C":
        console.log("Orta");
        break;
    case "D":
    case "F":
        console.log("Geliştirilmeli");
        break;
    default:
        console.log("Geçersiz not");
}
```

### Switch vs If-Else
```javascript
let yas = 25;

// Switch ile
switch (true) {
    case yas < 18:
        console.log("Reşit değilsiniz");
        break;
    case yas >= 18 && yas < 65:
        console.log("Yetişkinsiniz");
        break;
    case yas >= 65:
        console.log("Emeklisiniz");
        break;
    default:
        console.log("Geçersiz yaş");
}

// If-else ile (daha uygun)
if (yas < 18) {
    console.log("Reşit değilsiniz");
} else if (yas >= 18 && yas < 65) {
    console.log("Yetişkinsiniz");
} else if (yas >= 65) {
    console.log("Emeklisiniz");
} else {
    console.log("Geçersiz yaş");
}
```

### Switch Örnekleri
```javascript
// Haftanın günlerini kontrol etme
function gunKontrol(gun) {
    switch (gun.toLowerCase()) {
        case "pazartesi":
        case "salı":
        case "çarşamba":
        case "perşembe":
        case "cuma":
            return "İş günü";
        case "cumartesi":
        case "pazar":
            return "Hafta sonu";
        default:
            return "Geçersiz gün";
    }
}

console.log(gunKontrol("Pazartesi")); // "İş günü"
console.log(gunKontrol("Cumartesi")); // "Hafta sonu"
console.log(gunKontrol("xyz")); // "Geçersiz gün"

// Mevsim kontrolü
function mevsimKontrol(ay) {
    switch (ay) {
        case 12:
        case 1:
        case 2:
            return "Kış";
        case 3:
        case 4:
        case 5:
            return "İlkbahar";
        case 6:
        case 7:
        case 8:
            return "Yaz";
        case 9:
        case 10:
        case 11:
            return "Sonbahar";
        default:
            return "Geçersiz ay";
    }
}

console.log(mevsimKontrol(1));  // "Kış"
console.log(mevsimKontrol(6));  // "Yaz"
console.log(mevsimKontrol(13)); // "Geçersiz ay"
```

---

## 💻 Pratik Örnekler

### Örnek 1: Hesap Makinesi
```html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hesap Makinesi</title>
</head>
<body>
    <h1>Basit Hesap Makinesi</h1>
    
    <input type="number" id="sayi1" placeholder="İlk sayı">
    <select id="islem">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">×</option>
        <option value="/">÷</option>
    </select>
    <input type="number" id="sayi2" placeholder="İkinci sayı">
    <button onclick="hesapla()">Hesapla</button>
    
    <p id="sonuc"></p>

    <script>
        function hesapla() {
            let sayi1 = parseFloat(document.getElementById('sayi1').value);
            let sayi2 = parseFloat(document.getElementById('sayi2').value);
            let islem = document.getElementById('islem').value;
            let sonuc;

            switch (islem) {
                case '+':
                    sonuc = sayi1 + sayi2;
                    break;
                case '-':
                    sonuc = sayi1 - sayi2;
                    break;
                case '*':
                    sonuc = sayi1 * sayi2;
                    break;
                case '/':
                    if (sayi2 === 0) {
                        sonuc = "Sıfıra bölünemez!";
                    } else {
                        sonuc = sayi1 / sayi2;
                    }
                    break;
                default:
                    sonuc = "Geçersiz işlem";
            }

            document.getElementById('sonuc').textContent = `Sonuç: ${sonuc}`;
        }
    </script>
</body>
</html>
```

### Örnek 2: To-Do List
```html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
</head>
<body>
    <h1>To-Do List</h1>
    
    <input type="text" id="gorev" placeholder="Yeni görev ekle">
    <button onclick="gorevEkle()">Ekle</button>
    
    <ul id="gorevListesi"></ul>

    <script>
        let gorevler = [];

        function gorevEkle() {
            let gorevMetni = document.getElementById('gorev').value.trim();
            
            if (gorevMetni !== '') {
                gorevler.push(gorevMetni);
                document.getElementById('gorev').value = '';
                gorevleriGoster();
            }
        }

        function gorevSil(index) {
            gorevler.splice(index, 1);
            gorevleriGoster();
        }

        function gorevleriGoster() {
            let liste = document.getElementById('gorevListesi');
            liste.innerHTML = '';
            
            gorevler.forEach((gorev, index) => {
                let li = document.createElement('li');
                li.textContent = gorev;
                
                let silButon = document.createElement('button');
                silButon.textContent = 'Sil';
                silButon.onclick = () => gorevSil(index);
                
                li.appendChild(silButon);
                liste.appendChild(li);
            });
        }

        // Enter tuşu ile görev ekleme
        document.getElementById('gorev').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                gorevEkle();
            }
        });
    </script>
</body>
</html>
```

---



## 🔧 Faydalı Araçlar ve Kaynaklar

### Online Editörler:
- [CodePen](https://codepen.io/)
- [JSFiddle](https://jsfiddle.net/)
- [Replit](https://replit.com/)


## 📝 Önemli Notlar

### JavaScript En İyi Uygulamaları:
1. **Değişken isimlendirme** - Anlamlı ve açıklayıcı isimler kullanın
2. **Kod yorumları** - Karmaşık kodları açıklayın
3. **Hata kontrolü** - Kullanıcı girişlerini doğrulayın
4. **Kod organizasyonu** - Fonksiyonları mantıklı gruplandırın
5. **Modern syntax** - ES6+ özelliklerini kullanın

### Yaygın Hatalar:
- Değişken tanımlamadan kullanma
- Fonksiyon parametrelerini kontrol etmeme
- Sonsuz döngü oluşturma
- Tip kontrolü yapmama
- Global değişkenleri aşırı kullanma
