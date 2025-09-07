# JavaScript İleri Seviye - Eğitim Materyali

## 📚 İçindekiler
- [Fonksiyonlar](#fonksiyonlar)
- [Nesneler (Objects)](#nesneler-objects)
- [Döngüler (Loops)](#döngüler-loops)
- [Rastgele Sayılar](#rastgele-sayılar)
- [parseInt Fonksiyonu](#parseint-fonksiyonu)
- [Ternary Operatör](#ternary-operatör)
- [var vs let vs const](#var-vs-let-vs-const)
- [Arrow Functions](#arrow-functions)
- [Modern JavaScript Özellikleri](#modern-javascript-özellikleri)
- [ES6+ Özellikleri](#es6-özellikleri)
- [Class Syntax](#class-syntax)
- [Import/Export](#importexport)

---

## ⚙️ Fonksiyonlar

### Boolean Değer Döndüren Fonksiyonlar
```javascript
// Boolean değer döndüren fonksiyon
function isEven(num) {
    return num % 2 === 0;
}

console.log(isEven(4));  // true
console.log(isEven(7));  // false

// Yaş kontrolü
function isAdult(age) {
    return age >= 18;
}

console.log(isAdult(20)); // true
console.log(isAdult(16)); // false
```

### Return Early Pattern
```javascript
// Return early pattern - erken çıkış
function validateEmail(email) {
    if (!email) {
        return false;
    }
    
    if (!email.includes('@')) {
        return false;
    }
    
    if (email.length < 5) {
        return false;
    }
    
    return true;
}

console.log(validateEmail("test@example.com")); // true
console.log(validateEmail("invalid"));          // false
```

### Fonksiyon Örnekleri
```javascript
// Kart sayma oyunu
function countingCards(card) {
    let count = 0;
    
    switch(card) {
        case 2:
        case 3:
        case 4:
        case 5:
        case 6:
            count++;
            break;
        case 10:
        case 'J':
        case 'Q':
        case 'K':
        case 'A':
            count--;
            break;
    }
    
    if (count > 0) {
        return count + " Bet";
    } else {
        return count + " Hold";
    }
}

console.log(countingCards(2)); // "1 Bet"
console.log(countingCards('K')); // "-1 Hold"
```

---

## 🏗️ Nesneler (Objects)

### Nesne Oluşturma
```javascript
// Nesne oluşturma
let kullanici = {
    isim: "Faruk",
    yas: 20,
    meslek: "Web Geliştirici",
    aktif: true
};

console.log(kullanici);
```

### Dot Notation (Nokta Notasyonu)
```javascript
let kullanici = {
    isim: "Faruk",
    yas: 20
};

// Dot notation ile erişim
console.log(kullanici.isim);  // "Faruk"
console.log(kullanici.yas);   // 20

// Dot notation ile değiştirme
kullanici.yas = 21;
console.log(kullanici.yas);   // 21
```

### Bracket Notation (Köşeli Parantez Notasyonu)
```javascript
let kullanici = {
    isim: "Faruk",
    yas: 20
};

// Bracket notation ile erişim
console.log(kullanici["isim"]); // "Faruk"
console.log(kullanici["yas"]);  // 20

// Değişken ile erişim
let property = "isim";
console.log(kullanici[property]); // "Faruk"
```

### Nesne Özelliklerini Güncelleme
```javascript
let kullanici = {
    isim: "Faruk",
    yas: 20,
    meslek: "Öğrenci"
};

// Özellik güncelleme
kullanici.meslek = "Web Geliştirici";
kullanici.yas = 21;

console.log(kullanici);
```

### Yeni Özellik Ekleme
```javascript
let kullanici = {
    isim: "Faruk",
    yas: 20
};

// Yeni özellik ekleme
kullanici.email = "faruk@example.com";
kullanici["telefon"] = "555-1234";

console.log(kullanici);
```

### Özellik Silme
```javascript
let kullanici = {
    isim: "Faruk",
    yas: 20,
    meslek: "Web Geliştirici"
};

// Özellik silme
delete kullanici.meslek;
delete kullanici["yas"];

console.log(kullanici); // { isim: "Faruk" }
```

### Nesneleri Lookup (Arama) İçin Kullanma
```javascript
// Telefon kodları lookup
let telefonKodlari = {
    "ankara": 312,
    "istanbul": 212,
    "izmir": 232,
    "bursa": 224
};

function getSehirKodu(sehir) {
    return telefonKodlari[sehir.toLowerCase()];
}

console.log(getSehirKodu("Ankara")); // 312
console.log(getSehirKodu("İstanbul")); // 212
```

### Nesne Özelliklerini Test Etme
```javascript
let kullanici = {
    isim: "Faruk",
    yas: 20
};

// hasOwnProperty ile kontrol
console.log(kullanici.hasOwnProperty("isim")); // true
console.log(kullanici.hasOwnProperty("email")); // false

// in operatörü ile kontrol
console.log("yas" in kullanici); // true
console.log("meslek" in kullanici); // false
```

### Karmaşık Nesneler
```javascript
let koleksiyon = {
    "2548": {
        "album": "Slippery When Wet",
        "artist": "Bon Jovi",
        "tracks": ["Let It Rock", "You Give Love a Bad Name"]
    },
    "2468": {
        "album": "1999",
        "artist": "Prince",
        "tracks": ["1999", "Little Red Corvette"]
    },
    "1245": {
        "artist": "Robert Palmer",
        "tracks": []
    },
    "5439": {
        "album": "ABBA Gold"
    }
};

// Koleksiyon güncelleme fonksiyonu
function updateRecords(id, prop, value) {
    if (value === "") {
        delete koleksiyon[id][prop];
    } else if (prop === "tracks") {
        koleksiyon[id][prop] = koleksiyon[id][prop] || [];
        koleksiyon[id][prop].push(value);
    } else {
        koleksiyon[id][prop] = value;
    }
    
    return koleksiyon;
}

updateRecords(5439, "artist", "ABBA");
console.log(koleksiyon[5439]);
```

### İç İçe Nesneler
```javascript
let kullanici = {
    isim: "Faruk",
    yas: 20,
    adres: {
        sehir: "Ankara",
        mahalle: "Çankaya",
        postaKodu: "06100"
    },
    hobiler: ["okuma", "yazma", "kodlama"]
};

// İç içe nesneye erişim
console.log(kullanici.adres.sehir); // "Ankara"
console.log(kullanici.hobiler[0]);  // "okuma"
```

---

## 🔄 Döngüler (Loops)

### While Döngüsü
```javascript
let i = 0;
while (i < 5) {
    console.log("Sayı: " + i);
    i++;
}

// Sonsuz döngü örneği (dikkatli kullanın!)
// while (true) {
//     console.log("Sonsuz döngü!");
// }
```

### For Döngüsü
```javascript
// Temel for döngüsü
for (let i = 0; i < 5; i++) {
    console.log("Sayı: " + i);
}

// Tek sayılar
for (let i = 1; i <= 10; i += 2) {
    console.log("Tek sayı: " + i);
}

// Geriye sayma
for (let i = 10; i >= 1; i--) {
    console.log("Geriye sayma: " + i);
}
```

### Dizi ile For Döngüsü
```javascript
let renkler = ["kırmızı", "mavi", "yeşil", "sarı"];

for (let i = 0; i < renkler.length; i++) {
    console.log("Renk " + (i + 1) + ": " + renkler[i]);
}
```

### İç İçe For Döngüleri
```javascript
// Çarpım tablosu
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 3; j++) {
        console.log(i + " x " + j + " = " + (i * j));
    }
}

// Matris örneği
let matris = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

for (let i = 0; i < matris.length; i++) {
    for (let j = 0; j < matris[i].length; j++) {
        console.log("Matris[" + i + "][" + j + "] = " + matris[i][j]);
    }
}
```

### Do...While Döngüsü
```javascript
let i = 0;
do {
    console.log("Sayı: " + i);
    i++;
} while (i < 5);

// En az bir kez çalışır
let sayi = 10;
do {
    console.log("Bu her zaman çalışır: " + sayi);
    sayi++;
} while (sayi < 5);
```

### Profil Arama Örneği
```javascript
let contacts = [
    {
        "firstName": "Faruk",
        "lastName": "Güvenkaya",
        "number": "0544-123-4567",
        "likes": ["Pizza", "Coding", "Brownie Points"]
    },
    {
        "firstName": "Ayşe",
        "lastName": "Demir",
        "number": "0544-987-6543",
        "likes": ["Hogwarts", "Magic", "Hagrid"]
    }
];

function lookUpProfile(name, prop) {
    for (let i = 0; i < contacts.length; i++) {
        if (contacts[i].firstName === name) {
            if (contacts[i].hasOwnProperty(prop)) {
                return contacts[i][prop];
            } else {
                return "No such property";
            }
        }
    }
    return "No such contact";
}

console.log(lookUpProfile("Faruk", "likes")); // ["Pizza", "Coding", "Brownie Points"]
console.log(lookUpProfile("Ayşe", "number")); // "0544-987-6543"
```

---

## 🎲 Rastgele Sayılar

### Rastgele Kesirli Sayılar
```javascript
// 0 ile 1 arasında rastgele sayı
let rastgeleKesir = Math.random();
console.log(rastgeleKesir); // 0.123456789...

// 0 ile 9 arasında rastgele tam sayı
let rastgeleTam = Math.floor(Math.random() * 10);
console.log(rastgeleTam); // 0-9 arası
```

### Belirli Aralıkta Rastgele Sayı
```javascript
// min ile max arasında rastgele sayı
function rastgeleSayi(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

console.log(rastgeleSayi(1, 10));   // 1-10 arası
console.log(rastgeleSayi(50, 100)); // 50-100 arası
```

### Rastgele String Üretme
```javascript
function rastgeleString(uzunluk) {
    let karakterler = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
    let sonuc = "";
    
    for (let i = 0; i < uzunluk; i++) {
        sonuc += karakterler.charAt(Math.floor(Math.random() * karakterler.length));
    }
    
    return sonuc;
}

console.log(rastgeleString(8)); // "A3fK9mP2"
```

---

## 🔢 parseInt Fonksiyonu

### parseInt Temel Kullanımı
```javascript
// String'i sayıya çevirme
let str1 = "123";
let num1 = parseInt(str1);
console.log(num1); // 123

let str2 = "123abc";
let num2 = parseInt(str2);
console.log(num2); // 123 (sadece sayı kısmını alır)

let str3 = "abc123";
let num3 = parseInt(str3);
console.log(num3); // NaN (sayı ile başlamıyor)
```

### Radix (Taban) Parametresi
```javascript
// Binary (2'lik taban)
console.log(parseInt("1010", 2)); // 10

// Octal (8'lik taban)
console.log(parseInt("17", 8)); // 15

// Hexadecimal (16'lık taban)
console.log(parseInt("FF", 16)); // 255

// Varsayılan (10'luk taban)
console.log(parseInt("123")); // 123
```

### parseInt vs Number
```javascript
let str = "123abc";

console.log(parseInt(str)); // 123
console.log(Number(str));   // NaN
console.log(+str);          // NaN

let str2 = "123";
console.log(parseInt(str2)); // 123
console.log(Number(str2));   // 123
console.log(+str2);          // 123
```

---

## ❓ Ternary Operatör

### Temel Ternary Operatör
```javascript
let yas = 20;
let durum = yas >= 18 ? "Yetişkin" : "Çocuk";
console.log(durum); // "Yetişkin"

// If-else karşılaştırması
if (yas >= 18) {
    durum = "Yetişkin";
} else {
    durum = "Çocuk";
}
```

### Çoklu Ternary Operatör
```javascript
let not = 85;
let harfNotu = not >= 90 ? "A" : 
               not >= 80 ? "B" : 
               not >= 70 ? "C" : 
               not >= 60 ? "D" : "F";

console.log(harfNotu); // "B"

// If-else if karşılaştırması
if (not >= 90) {
    harfNotu = "A";
} else if (not >= 80) {
    harfNotu = "B";
} else if (not >= 70) {
    harfNotu = "C";
} else if (not >= 60) {
    harfNotu = "D";
} else {
    harfNotu = "F";
}
```

### Ternary ile Fonksiyon
```javascript
function checkSign(num) {
    return num > 0 ? "pozitif" : 
           num < 0 ? "negatif" : "sıfır";
}

console.log(checkSign(5));  // "pozitif"
console.log(checkSign(-3)); // "negatif"
console.log(checkSign(0));  // "sıfır"
```

---

## 🔄 var vs let vs const

### var Kullanımı
```javascript
// var - function scope
function testVar() {
    if (true) {
        var x = 1;
    }
    console.log(x); // 1 (erişilebilir)
}

// var - hoisting
console.log(y); // undefined (hata vermez)
var y = 5;

// var - yeniden tanımlama
var z = 1;
var z = 2; // Hata vermez
console.log(z); // 2
```

### let Kullanımı
```javascript
// let - block scope
function testLet() {
    if (true) {
        let x = 1;
    }
    // console.log(x); // Hata! x tanımlı değil
}

// let - hoisting
// console.log(y); // Hata! Cannot access 'y' before initialization
let y = 5;

// let - yeniden tanımlama
let z = 1;
// let z = 2; // Hata! 'z' has already been declared
```

### const Kullanımı
```javascript
// const - sabit değer
const PI = 3.14159;
// PI = 3.14; // Hata! Assignment to constant variable

// const - object
const kullanici = {
    isim: "Faruk",
    yas: 25
};

kullanici.yas = 26; // OK - object property değiştirilebilir
// kullanici = {}; // Hata! object'in kendisi değiştirilemez

// const - array
const renkler = ["kırmızı", "mavi"];
renkler.push("yeşil"); // OK - array'e eleman eklenebilir
// renkler = []; // Hata! array'in kendisi değiştirilemez
```

### Object.freeze() ile Değişikliği Önleme
```javascript
const kullanici = Object.freeze({
    isim: "Faruk",
    yas: 25
});

// kullanici.yas = 26; // Hata vermez ama değişmez
console.log(kullanici.yas); // 25

// Nested object'ler için deep freeze gerekir
const deepFreeze = (obj) => {
    Object.keys(obj).forEach(prop => {
        if (typeof obj[prop] === 'object') {
            deepFreeze(obj[prop]);
        }
    });
    return Object.freeze(obj);
};
```

---

## ➡️ Arrow Functions

### Temel Arrow Function
```javascript
// Geleneksel fonksiyon
function topla(a, b) {
    return a + b;
}

// Arrow function
const toplaArrow = (a, b) => {
    return a + b;
};

// Tek satır arrow function
const toplaKisa = (a, b) => a + b;

console.log(topla(2, 3));        // 5
console.log(toplaArrow(2, 3));   // 5
console.log(toplaKisa(2, 3));    // 5
```

### Tek Parametre
```javascript
// Parantez olmadan
const kare = x => x * x;

// Parantez ile
const kare2 = (x) => x * x;

console.log(kare(5)); // 25
```

### Parametresiz
```javascript
const selamla = () => "Merhaba!";
console.log(selamla()); // "Merhaba!"
```

### this Bağlamı
```javascript
// Geleneksel fonksiyon - kendi this'i var
let obj1 = {
    isim: "Faruk",
    selamla: function() {
        console.log("Merhaba " + this.isim);
    }
};

// Arrow function - this'i yok, dış scope'dan alır
let obj2 = {
    isim: "Faruk",
    selamla: () => {
        console.log("Merhaba " + this.isim); // undefined
    }
};

obj1.selamla(); // "Merhaba Faruk"
obj2.selamla(); // "Merhaba undefined"
```

---

## 🚀 Modern JavaScript Özellikleri

### Default Parameters
```javascript
// Varsayılan parametreler
function selamla(isim = "Misafir", mesaj = "Merhaba") {
    return `${mesaj} ${isim}!`;
}

console.log(selamla());                    // "Merhaba Misafir!"
console.log(selamla("Faruk"));            // "Merhaba Faruk!"
console.log(selamla("Faruk", "Selam"));   // "Selam Faruk!"
```

### Rest Operator (...)
```javascript
// Rest operator - kalan parametreleri toplar
function topla(...sayilar) {
    return sayilar.reduce((toplam, sayi) => toplam + sayi, 0);
}

console.log(topla(1, 2, 3, 4, 5)); // 15

// Destructuring ile rest
const [ilk, ikinci, ...kalan] = [1, 2, 3, 4, 5];
console.log(ilk);    // 1
console.log(ikinci); // 2
console.log(kalan);  // [3, 4, 5]
```

### Spread Operator (...)
```javascript
// Array'leri birleştirme
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const birlesik = [...arr1, ...arr2];
console.log(birlesik); // [1, 2, 3, 4, 5, 6]

// Object'leri birleştirme
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const birlesikObj = { ...obj1, ...obj2 };
console.log(birlesikObj); // { a: 1, b: 2, c: 3, d: 4 }

// Fonksiyon çağrısında spread
function topla(a, b, c) {
    return a + b + c;
}

const sayilar = [1, 2, 3];
console.log(topla(...sayilar)); // 6
```

### Destructuring Assignment
```javascript
// Array destructuring
const renkler = ["kırmızı", "mavi", "yeşil"];
const [renk1, renk2, renk3] = renkler;
console.log(renk1); // "kırmızı"

// Object destructuring
const kullanici = {
    isim: "Faruk",
    yas: 25,
    meslek: "Web Geliştirici"
};

const { isim, yas, meslek } = kullanici;
console.log(isim); // "Faruk"

// Yeniden adlandırma
const { isim: kullaniciAdi, yas: kullaniciYasi } = kullanici;
console.log(kullaniciAdi); // "Faruk"

// Varsayılan değerler
const { isim: ad = "Bilinmiyor", sehir = "Ankara" } = kullanici;
console.log(ad);    // "Faruk"
console.log(sehir); // "Ankara"
```

---

## 📝 ES6+ Özellikleri

### Template Literals
```javascript
const isim = "Faruk";
const yas = 20;

// Geleneksel string birleştirme
const mesaj1 = "Merhaba " + isim + ", yaşınız " + yas;

// Template literal
const mesaj2 = `Merhaba ${isim}, yaşınız ${yas}`;

// Çok satırlı string
const cokSatirli = `
    Merhaba ${isim},
    Yaşınız: ${yas}
    Hoş geldiniz!
`;

console.log(mesaj1);
console.log(mesaj2);
console.log(cokSatirli);
```

### Simple Fields
```javascript
const isim = "Faruk";
const yas = 20;

// Geleneksel object
const kullanici1 = {
    isim: isim,
    yas: yas,
    selamla: function() {
        return "Merhaba!";
    }
};

// Simple fields
const kullanici2 = {
    isim,
    yas,
    selamla() {
        return "Merhaba!";
    }
};

console.log(kullanici1);
console.log(kullanici2);
```

### Declarative Functions
```javascript
// Function declaration
function topla(a, b) {
    return a + b;
}

// Function expression
const topla2 = function(a, b) {
    return a + b;
};

// Arrow function
const topla3 = (a, b) => a + b;

// Method shorthand (ES6)
const hesap = {
    topla(a, b) {
        return a + b;
    },
    cikar(a, b) {
        return a - b;
    }
};
```

---

## 🏛️ Class Syntax

### Temel Class
```javascript
class Kullanici {
    constructor(isim, yas) {
        this.isim = isim;
        this.yas = yas;
    }
    
    selamla() {
        return `Merhaba, ben ${this.isim}`;
    }
    
    yasArtir() {
        this.yas++;
    }
}

const kullanici = new Kullanici("Faruk", 20);
console.log(kullanici.selamla()); // "Merhaba, ben Faruk"
kullanici.yasArtir();
console.log(kullanici.yas); // 21
```

### Inheritance (Kalıtım)
```javascript
class Kullanici {
    constructor(isim, yas) {
        this.isim = isim;
        this.yas = yas;
    }
    
    selamla() {
        return `Merhaba, ben ${this.isim}`;
    }
}

class Admin extends Kullanici {
    constructor(isim, yas, yetki) {
        super(isim, yas);
        this.yetki = yetki;
    }
    
    adminSelamla() {
        return `${this.selamla()} ve ben adminim`;
    }
}

const admin = new Admin("Faruk", 20, "full");
console.log(admin.adminSelamla());
```

### Getters ve Setters
```javascript
class Daire {
    constructor(yaricap) {
        this._yaricap = yaricap;
    }
    
    get yaricap() {
        return this._yaricap;
    }
    
    set yaricap(deger) {
        if (deger < 0) {
            throw new Error("Yarıçap negatif olamaz");
        }
        this._yaricap = deger;
    }
    
    get alan() {
        return Math.PI * this._yaricap * this._yaricap;
    }
    
    get cevre() {
        return 2 * Math.PI * this._yaricap;
    }
}

const daire = new Daire(5);
console.log(daire.alan);   // 78.54...
console.log(daire.cevre);  // 31.41...

daire.yaricap = 10;
console.log(daire.alan);   // 314.15...
```

---

## 📦 Import/Export

### Named Export
```javascript
// math.js
export const PI = 3.14159;

export function topla(a, b) {
    return a + b;
}

export function cikar(a, b) {
    return a - b;
}

// main.js
import { PI, topla, cikar } from './math.js';

console.log(PI);           // 3.14159
console.log(topla(2, 3));  // 5
console.log(cikar(5, 2));  // 3
```

### Default Export
```javascript
// Kullanici.js
class Kullanici {
    constructor(isim) {
        this.isim = isim;
    }
}

export default Kullanici;

// main.js
import Kullanici from './Kullanici.js';

const kullanici = new Kullanici("Faruk");
```

### Mixed Export
```javascript
// utils.js
export const VERSION = "1.0.0";

export function formatDate(date) {
    return date.toLocaleDateString();
}

export default class Utils {
    static formatTime(time) {
        return time.toLocaleTimeString();
    }
}

// main.js
import Utils, { VERSION, formatDate } from './utils.js';

console.log(VERSION);
console.log(formatDate(new Date()));
console.log(Utils.formatTime(new Date()));
```

---

## 🏃‍♂️ Alıştırmalar

### Alıştırma 1: Hesap Makinesi
```javascript
// Bir hesap makinesi sınıfı oluşturun
class HesapMakinesi {
    constructor() {
        this.sonuc = 0;
    }
    
    topla(sayi) {
        this.sonuc += sayi;
        return this;
    }
    
    cikar(sayi) {
        this.sonuc -= sayi;
        return this;
    }
    
    carp(sayi) {
        this.sonuc *= sayi;
        return this;
    }
    
    bol(sayi) {
        if (sayi === 0) {
            throw new Error("Sıfıra bölünemez");
        }
        this.sonuc /= sayi;
        return this;
    }
    
    temizle() {
        this.sonuc = 0;
        return this;
    }
    
    getSonuc() {
        return this.sonuc;
    }
}

// Kullanım
const hesap = new HesapMakinesi();
const sonuc = hesap.topla(10).carp(2).cikar(5).getSonuc();
console.log(sonuc); // 15
```

### Alıştırma 2: Todo List
```javascript
class TodoList {
    constructor() {
        this.gorevler = [];
    }
    
    gorevEkle(gorev) {
        const yeniGorev = {
            id: Date.now(),
            metin: gorev,
            tamamlandi: false,
            tarih: new Date()
        };
        this.gorevler.push(yeniGorev);
        return yeniGorev;
    }
    
    gorevSil(id) {
        this.gorevler = this.gorevler.filter(gorev => gorev.id !== id);
    }
    
    gorevTamamla(id) {
        const gorev = this.gorevler.find(g => g.id === id);
        if (gorev) {
            gorev.tamamlandi = true;
        }
    }
    
    tamamlananGorevler() {
        return this.gorevler.filter(gorev => gorev.tamamlandi);
    }
    
    bekleyenGorevler() {
        return this.gorevler.filter(gorev => !gorev.tamamlandi);
    }
}

// Kullanım
const todo = new TodoList();
todo.gorevEkle("JavaScript öğren");
todo.gorevEkle("Proje yap");
todo.gorevTamamla(todo.gorevler[0].id);
console.log(todo.bekleyenGorevler());
```

### Alıştırma 3: Oyun Sınıfı
```javascript
class Oyun {
    constructor(oyuncuAdi) {
        this.oyuncuAdi = oyuncuAdi;
        this.skor = 0;
        this.seviye = 1;
        this.can = 3;
    }
    
    puanEkle(puan) {
        this.skor += puan;
        if (this.skor >= this.seviye * 100) {
            this.seviyeArtir();
        }
    }
    
    seviyeArtir() {
        this.seviye++;
        this.can++;
        console.log(`Seviye ${this.seviye}! +1 can`);
    }
    
    canKaybet() {
        this.can--;
        if (this.can <= 0) {
            this.oyunBitti();
        }
    }
    
    oyunBitti() {
        console.log(`Oyun bitti! Skor: ${this.skor}, Seviye: ${this.seviye}`);
    }
    
    oyunBilgisi() {
        return {
            oyuncu: this.oyuncuAdi,
            skor: this.skor,
            seviye: this.seviye,
            can: this.can
        };
    }
}

// Kullanım
const oyun = new Oyun("Faruk");
oyun.puanEkle(50);
oyun.puanEkle(60);
console.log(oyun.oyunBilgisi());
```
