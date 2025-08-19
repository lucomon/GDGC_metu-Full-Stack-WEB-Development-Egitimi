# JavaScript Temelleri – README

Bu doküman, JavaScript’e yeni başlayanlar için temel konuları kısa, anlaşılır ve örnekli şekilde açıklar.

## İçindekiler
- [JavaScript’i çalıştırmak](#javascripte-çalıştırmak)
- [Temel data tipleri](#temel-data-tipleri)
- [Değişken tanımlama](#değişken-tanımlama)
- [Temel operatörler](#temel-operatörler)
- [Temel aritmetik operatörler](#temel-aritmetik-operatörler)
- [Strings](#strings)
- [Arrays](#arrays)
- [if/else ifadeleri](#ifelse-ifadeleri)
- [Logical operators](#logical-operators)
- [switch kullanımı](#switch-kullanımı)

---

## JavaScript’i çalıştırmak

- Tarayıcı Konsolu: Herhangi bir sayfada sağ tık → Inspect/İncele → Console → kodunuzu yazın.
- HTML içinde:

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

- Node.js ile (terminal):

```bash
node -v
node
> console.log("Merhaba Node");
```

- Online ortam: StackBlitz, CodeSandbox, JSFiddle gibi araçlarla hızlıca deneyin.

---

## Temel data tipleri

- Primitif: `number`, `string`, `boolean`, `null`, `undefined`, `bigint`, `symbol`
- Referans: `object` (diziler ve fonksiyonlar da nesnedir)
- `typeof` örnekleri:

```js
typeof 42;            // "number"
typeof "merhaba";     // "string"
typeof true;          // "boolean"
typeof undefined;     // "undefined"
typeof null;          // "object" (tarihsel bir hata ama gerçekte null)
typeof 10n;           // "bigint"
typeof Symbol();      // "symbol"
typeof { a: 1 };      // "object"
typeof [1, 2, 3];     // "object"
```

- `null` = “boş değer”; `undefined` = “atanmamış”.

---

## Değişken tanımlama

- `let`: blok kapsamlı, yeniden atanabilir.
- `const`: blok kapsamlı, yeniden atanamaz (referans aynı kalır; içeriği değişebilir).
- `var`: fonksiyon kapsamlı; hoisting ve kapsam sorunları yüzünden modern JS’te önerilmez.
- İsimlendirme: anlamlı, `camelCase`, harfle/alt çizgiyle başlayın.

```js
let sayac = 0;
const API_URL = "https://example.com";
sayac = sayac + 1;    // OK
// API_URL = "x";     // Hata
```

---

## Temel operatörler

- Atama: `=`, `+=`, `-=`, `*=`, `/=`, `%=` …
- Karşılaştırma: `===`, `!==`, `>`, `<`, `>=`, `<=`
  - `===` (tür ve değer eşitliği) önerilir. `==` dönüştürme yapar, sürpriz sonuçlara yol açabilir.
- Tür: `typeof x`
- Üçlü (ternary):

```js
const yas = 20;
const yetiskinMi = yas >= 18 ? "Evet" : "Hayır";
```

---

## Temel aritmetik operatörler

- `+ - * / % **`
- `++` (arttır), `--` (azalt) – ön-ek ve son-ek farkı vardır.

```js
5 + 2;     // 7
5 - 2;     // 3
5 * 2;     // 10
5 / 2;     // 2.5
5 % 2;     // 1 (mod)
2 ** 3;    // 8 (üs)

let x = 1;
x++;       // 2
++x;       // 3
```

- `+` string ile kullanılırsa birleştirme yapar:

```js
"JS " + "Güzel"; // "JS Güzel"
```

---

## Strings

- Tek tırnak, çift tırnak veya template literal (backtick) kullanılabilir.
- Template literal ile gömülü ifade ve çok satır:

```js
const ad = "Ada";
const yas = 25;
const mesaj = `Merhaba ${ad}, gelecek yıl ${yas + 1} yaşında olacaksın.`;
```

- Faydalı özellik ve metotlar:

```js
const s = "  Merhaba JS  ";
s.length;                 // 13
s[0];                     // " "
s.trim();                 // "Merhaba JS"
s.toUpperCase();          // "  MERHABA JS  "
s.includes("JS");         // true
s.indexOf("JS");          // 10
s.slice(2, 9);            // "Merhaba"
"ad-soyad".split("-");    // ["ad","soyad"]
"price: 10".replace("10","15"); // "price: 15"
```

---

## Arrays

- Oluşturma ve erişim:

```js
const sayilar = [10, 20, 30];
sayilar[0];        // 10
sayilar.length;    // 3
```

- Ekleme/çıkarma:

```js
const sepet = ["elma"];
sepet.push("armut");   // ["elma","armut"]
sepet.pop();           // ["elma"]
sepet.unshift("kiraz");// ["kiraz","elma"]
sepet.shift();         // ["elma"]
```

- Arama/kopya:

```js
[1,2,3].includes(2);    // true
[1,2,3].indexOf(3);     // 2
const kopya = [...sayilar]; // spread kopya
```

- Dilimleme/değiştirme:

```js
const a = [1,2,3,4,5];
a.slice(1,4);          // [2,3,4] (orijinali bozmaz)
a.splice(2,1,"X");     // [1,2,"X",4,5] (orijinali değiştirir)
```

- Dönüştürme/filtreleme/indirgeme:

```js
[1,2,3].map(n => n * 2);            // [2,4,6]
[1,2,3,4].filter(n => n % 2 === 0); // [2,4]
[1,2,3].reduce((toplam,n) => toplam + n, 0); // 6
```

- Döngü:

```js
for (const oge of ["a","b","c"]) {
  console.log(oge);
}
```

---

## if/else ifadeleri

- Yapı:

```js
const puan = 75;

if (puan >= 90) {
  console.log("AA");
} else if (puan >= 80) {
  console.log("BA");
} else if (puan >= 70) {
  console.log("BB");
} else {
  console.log("Geçti/Kaldı değerlendirmesi dışında");
}
```

- Truthy/Falsy:
  - Falsy: `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`
  - Diğer tüm değerler truthy kabul edilir.

```js
if ("") { /* çalışmaz */ }
if ("Merhaba") { /* çalışır */ }
```

---

## Logical operators

- `&&` (ve), `||` (veya), `!` (değil) – kısa devre mantığı kullanır.

```js
true && "x";     // "x"   (soldaki true ise sağdakini döner)
false && "x";    // false
false || "x";    // "x"   (soldaki falsy ise sağdakini döner)
"ad" || "varsayılan"; // "ad"
!"ad";           // false
```

- Nullish coalescing `??`: Sadece `null` veya `undefined` ise sağdakini döner.

```js
0 || 10;         // 10  (0 falsy olduğu için)
0 ?? 10;         // 0   (0 null/undefined değil)
undefined ?? 10; // 10
```

- Opsiyonel zincirleme `?.`: Ara değer `null/undefined` ise hatasız `undefined` döner.

```js
const kullanici = { profil: { ad: "Ada" } };
kullanici.profil?.ad;    // "Ada"
kullanici.adres?.sehir;  // undefined (hata atmaz)
```

---

## switch kullanımı

- Çoklu durum kontrolü için uygundur.

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

console.log(ad);
```

- `break` kullanmazsanız sonraki case’ler çalışmaya devam eder (fall-through).
- Fonksiyon içinde `return` kullanırsanız `break` gerekmez:

```js
function gunAdi(gun) {
  switch (gun) {
    case 1: return "Pazartesi";
    case 2: return "Salı";
    default: return "Bilinmiyor";
  }
}
```

---

## İpuçları

- Hata ayıklama için `console.log(...)` kullanın.
- Kodunuzu küçük parçalara bölün; fonksiyonlar yazın.
- Tutarlı biçimlendirme ve isimlendirme öğrenmeyi hızlandırır.
