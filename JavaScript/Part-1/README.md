# JavaScript Temelleri (Yeni Başlayanlar İçin) – README

Bu kılavuz, JavaScript’e sıfırdan başlayan birinin hızlı ve sağlam bir temel oluşturması için hazırlandı. Her bölümde “Nedir?”, “Nasıl kullanılır?” bulunur. Kodları tarayıcıda (Console) ya da Node.js ile çalıştırabilirsiniz.

## İçindekiler
- [JavaScript’i Çalıştırmak](#javascripti-çalıştırmak)
- [Temel Data Tipleri](#temel-data-tipleri)
- [Değişken Tanımlama](#değişken-tanımlama)
- [Temel Aritmetik Operatörler](#temel-aritmetik-operatörler)
- [Temel Operatörler](#temel-operatörler)
- [Strings](#strings)
- [Arrays](#arrays)
- [if/else İfadeleri](#ifelse-ifadeleri)
- [Logical Operators](#logical-operators)
- [switch Kullanımı](#switch-kullanımı)


---

## JavaScript’i Çalıştırmak

### Nedir?
JavaScript; web sayfalarına etkileşim kazandıran, tarayıcıda ve Node.js ile sunucu/araç tarafında da çalışabilen bir programlama dilidir.

### Nasıl kullanılır?
- Tarayıcı Konsolu: Herhangi bir sayfada sağ tık → İncele (Inspect) → Console sekmesi.
- HTML içinde (gömülü):
```html
<!doctype html>
<html>
  <body>
    <h1>Merhaba</h1>
    <script>
      console.log("JS çalıştı!");
    </script>
  </body>
</html>
```
- HTML içinde (harici dosya):
```html
<!doctype html>
<html>
  <head>
    <script src="app.js" defer></script>
  </head>
  <body>...</body>
</html>
```
- Node.js ile (terminal):
```bash
node -v      # sürümü gösterir
node         # REPL
> console.log("Merhaba Node");
```
- Online: StackBlitz, CodeSandbox, JSFiddle.

### İpuçları
- `defer`: Script, DOM yüklendikten sonra sırayla çalışır (önerilir). `async`: indirilir indirilmez çalışır (sıra garanti değil).
- Tarayıcı API’leri (alert, document) Node’da yoktur; Node’da çalıştırırsanız hata alırsınız.


---

## Temel Data Tipleri

### Nedir?
JavaScript’te iki ana kategori vardır:
- Primitif: `number`, `string`, `boolean`, `null`, `undefined`, `bigint`, `symbol`
- Referans: `object` (dizi ve fonksiyonlar dâhil)

### Nasıl kullanılır?
```js
typeof 42;            // "number"
typeof "merhaba";     // "string"
typeof true;          // "boolean"
typeof undefined;     // "undefined"
typeof null;          // "object" (tarihsel bir hata)
typeof 10n;           // "bigint"
typeof Symbol();      // "symbol"
typeof { a: 1 };      // "object"
typeof [1, 2, 3];     // "object" (diziler de nesnedir)
```



### Sık Hatalar
- `typeof null` → `"object"` gelmesi normaldir.
- `BigInt` ile `Number` toplanamaz: `1n + 1` hata verir.
- Ondalık aritmetiğinde küçük farklar olabilir (precision loss).

---

## Değişken Tanımlama

### Nedir?
Verileri isimlendirip saklamak için değişkenlere ihtiyaç duyarız.

### Nasıl kullanılır?
- `let`: blok kapsamlı, yeniden atanabilir.
- `const`: blok kapsamlı, yeniden atanamaz (referans sabit; içerik değişebilir).
- `var`: fonksiyon kapsamlı; modern JS’te önerilmez.
```js
let sayac = 0;
const API_URL = "https://example.com";
sayac = sayac + 1;    // OK
// API_URL = "x";     // Hata (referans)

const k = { ad: "Ada" };
k.ad = "Luna"; // OK (içerik değişti)
```

- Kapsam:
  - Blok (`{}`): `let/const` burada görünür.
  - Fonksiyon: `var` fonksiyon içi görünür.
- Hoisting ve "Temporal Dead Zone": `let/const` ile tanımdan önce erişmeyin.
- İsimlendirme: `camelCase`, anlamlı, harfle/alt çizgiyle başlayın.

### Sık Hatalar
- `var` beklenmedik kapsam sorunlarına yol açabilir.
- `const` ile atama yapılamaz; ama nesne/dizi içerikleri değişebilir.

### Alıştırma
- `const` ile bir dizi tanımlayın, `push` ile eleman ekleyin; çalıştığını gözlemleyin.

---
## Temel Aritmetik Operatörler

### Nedir?
Sayısal işlemler için kullanılır.

### Nasıl kullanılır?
- `+ - * / % **`
- `++` (arttır), `--` (azalt): ön ek ve son ek farkı vardır.
```js
5 + 2;     // 7
5 - 2;     // 3
5 * 2;     // 10
5 / 2;     // 2.5
5 % 2;     // 1 (kalan)
2 ** 3;    // 8 (üs)

let x = 1;
x++;        // 2 (sonra arttır)
++x;        // 3 (önce arttır)
```
- `+` string ile birleştirme yapar:
```js
"JS " + "Güzel";   // "JS Güzel"
"10" + 5;          // "105"
+"10" + 5;         // 15 (unary + ile sayıya çevirir)
```



---
## Temel Operatörler

### Nedir?
Atama, karşılaştırma ve mantıksal işlemleri ifade eden semboller.

### Nasıl kullanılır?
- Atama: `=`, `+=`, `-=`, `*=`, `/=`, `%=` ...
- Karşılaştırma: `===`, `!==`, `>`, `<`, `>=`, `<=`
```js
3 === 3;     // true
"3" === 3;   // false (tür farkı)
"3" == 3;    // true  (dönüşüm yapar, önerilmez)
```
- Üçlü (ternary):
```js
const yas = 20;
const yetiskin = yas >= 18 ? "Evet" : "Hayır";
```
- Tür: `typeof x`

---

## Strings

### Nedir?
Metinleri temsil eder. Değiştirilemezdir (immutable). İşlemler yeni string döndürür.

### Nasıl kullanılır?
```js
const ad = "Ada";
const yas = 25;
const mesaj = `Merhaba ${ad}, gelecek yıl ${yas + 1} yaşında olacaksın.`;
```
- Faydalı metotlar:
```js
const s = "  Merhaba JS  ";
s.length;                 // 13
s.trim();                 // "Merhaba JS"
s.toUpperCase();          // "  MERHABA JS  "
s.includes("JS");         // true
s.indexOf("JS");          // 10
s.slice(2, 9);            // "Merhaba"
"ad-soyad".split("-");    // ["ad","soyad"]
"price: 10".replace("10","15"); // "price: 15"
"deneme".startsWith("de"); // true
"deneme".endsWith("me");   // true
```
- Çok satır ve kaçışlar:
```js
const poem = `Satır 1\nSatır 2`;
```

---

## Arrays

### Nedir?
Sıralı veri koleksiyonları. Diziler de nesnedir.

### Nasıl kullanılır?
```js
const sayilar = [10, 20, 30];
sayilar[0];        // 10
sayilar.length;    // 3

const sepet = ["elma"];
sepet.push("armut");   // ["elma","armut"]
sepet.pop();            // ["elma"]
sepet.unshift("kiraz"); // başa ekler
sepet.shift();          // baştan alır
```
- Kopyalama ve birleştirme:
```js
const kopya = [...sayilar];
const birlesik = [...sayilar, 40, 50];
```
- Dilimleme/değiştirme:
```js
const a = [1,2,3,4,5];
a.slice(1,4);          // [2,3,4] (orijinal değişmez)
a.splice(2,1,"X");     // [1,2,"X",4,5] (orijinal değişir)
```
- Dönüştürme/filtreleme/indirgeme:
```js
[1,2,3].map(n => n * 2);            // [2,4,6]
[1,2,3,4].filter(n => n % 2 === 0); // [2,4]
[1,2,3].reduce((sum,n) => sum + n, 0); // 6
```
- Arama/doğrulama:
```js
const nums = [5, 10, 15];
nums.find(n => n > 8);       // 10
nums.findIndex(n => n > 8);  // 1
nums.some(n => n % 2 === 0); // true
nums.every(n => n > 0);      // true
```
- Sıralama (dikkat):
```js
[10, 2, 5].sort();            // [10,2,5] (metin gibi)
[10, 2, 5].sort((a,b) => a-b); // [2,5,10]
```
- İmmutable alternatifler (orijinali bozmadan):
```js
const arr = [3, 1, 2];
const s = arr.toSorted();   // [1,2,3]
const r = arr.toReversed(); // [2,1,3] -> örnek amaçlı
```

---

## if/else İfadeleri

### Nedir?
Koşula göre farklı kod yollarını çalıştırır.

### Nasıl kullanılır?
```js
const puan = 75;

if (puan >= 90) {
  console.log("AA");
} else if (puan >= 80) {
  console.log("BA");
} else if (puan >= 70) {
  console.log("BB");
} else {
  console.log("Diğer");
}
```
- Truthy/Falsy davranışı:
```js
if ("") { /* çalışmaz */ }
if ("Merhaba") { /* çalışır */ }
```
- Guard clause (erken çıkış) örneği:
```js
function login(user) {
  if (!user) return "Kullanıcı yok";
  if (!user.active) return "Hesap pasif";
  return "Giriş başarılı";
}
```

---

## Logical Operators

### Nedir?
Mantıksal işlemler ve kısa devre davranışı.

### Nasıl kullanılır?
- `&&` (ve), `||` (veya), `!` (değil)
```js
true && "x";      // "x"   (soldaki true ise sağdakini döner)
false && "x";     // false
false || "x";     // "x"   (soldaki falsy ise sağdakini döner)
"ad" || "vars";   // "ad"
!"ad";            // false
```
- Nullish coalescing `??`: Yalnızca `null/undefined` için yedek değer döner.
```js
0 || 10;          // 10  (0 falsy)
0 ?? 10;          // 0   (0 null/undefined değil)
undefined ?? 10;  // 10
```
- Opsiyonel zincirleme `?.` ve opsiyonel çağrı:
```js
const u = { profil: { ad: "Ada" } };
u.profil?.ad;      // "Ada"
u.adres?.sehir;    // undefined (hatasız)
obj.method?.();    // varsa çağır
arr?.[0];          // varsa ilk eleman
```
- Atama varyantları: `||=`, `&&=`, `??=`
```js
let cache = null;
cache ||= {};    // cache falsy ise yeni obje ata
let name;
name ??= "Anonim"; // yalnızca name null/undefined ise ata
```
---

## switch Kullanımı

### Nedir?
Çoklu durum kontrolü için uygundur.

### Nasıl kullanılır?
```js
const gun = 3;
let ad;

switch (gun) {
  case 1:
    ad = "Pazartesi";
    break;
  case 2:
    ad = "Salı";
    break;
  case 3:
  case 4:
    ad = "Çarşamba veya Perşembe"; // fall-through
    break;
  default:
    ad = "Bilinmiyor";
}
```
- Fonksiyon içinde `return` kullanırsanız `break` gerekmez.
```js
function gunAdi(g) {
  switch (g) {
    case 1: return "Pazartesi";
    case 2: return "Salı";
    default: return "Bilinmiyor";
  }
}
```
- Alternatif (harita):
```js
const isim = {1: "Pzt", 2: "Sal"}[gun] ?? "?";
```
