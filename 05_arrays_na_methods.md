# Module 05: Arrays & Array Methods

Karibu lesson five! Kufikia sasa tumeelewa venye functions zinafanya kazi. Sasa ni time ya kuingia kwenye mojawapo(hapa nimekua Ken Walibora) ya data structures muhimu zaidi kwa maisha ya developer: **Arrays**.

Fikiria **array** kama tray ya mayai, list ya shopping, au trolley ya supermarket. Badala ya kudeclare variables mia moja tofauti kwa kila kitu unachonunua (`const item1 = "Mkate"`, `const item2 = "Maziwa"`, `const item3 = "Mayai"` — utajaza memory na code bila sababu!), unaweka vitu zote ndani ya chombo kimoja ukitumia **square brackets `[]`** na kuseparate kila item na comma (`,`).

```javascript
const shoppingList = ["Mkate", "Maziwa", "Mayai", "Sukari"];
```

---

## 1. Zero-Based Indexing & Accessing Elements 🔢

Kitu cha kwanza unachofaa kujua ni kwamba: **computer inaanza kuhesabu kuanzia 0, si 1!**

Hiyo position ya item ndani ya array inaitwa **index**:

| Item | `"Mkate"` | `"Maziwa"` | `"Mayai"` | `"Sukari"` |
| :---: | :---: | :---: | :---: | :---: |
| **Index** | `0` | `1` | `2` | `3` |

### Mfano kwa Vitendo:
```javascript
const mitaa = ["Rongai", "Westlands", "Kilimani", "Kibera"];

console.log(mitaa[0]); // "Rongai" (Item ya kwanza)
console.log(mitaa[2]); // "Kilimani" (Item ya tatu)

// Kujua idadi ya items ndani ya array tunatumia .length:
console.log(mitaa.length); // 4

// Ku-access item ya mwisho kabisa:
console.log(mitaa[mitaa.length - 1]); // "Kibera"
```

---

## 2. Adding and Removing Elements (`push`, `pop`, `shift`, `unshift`) 🧰

JavaScript inakuja na methods za ndani (built-in methods) za ku-manipulate array:

* **`.push(item)`**: Inaongeza item mpya pale **mwishoni** mwa array.
* **`.pop()`**: Inatoa na kutupa ile item ya **mwisho kabisa**.
* **`.unshift(item)`**: Inaongeza item mpya pale **mwanzoni**.
* **`.shift()`**: Inatoa na kutupa ile item ya **kwanza kabisa**.
* **`.includes(item)`**: Inacheck kama kitu kiko ndani ya array (inareturn `true` au `false`).

```javascript
const squad = ["Brian", "Kevin", "Otieno"];

squad.push("Mwangi"); // Inaongeza Mwangi mwishoni
console.log(squad);   // ["Brian", "Kevin", "Otieno", "Mwangi"]

squad.pop();          // Inamtoa Mwangi
console.log(squad);   // ["Brian", "Kevin", "Otieno"]

console.log(squad.includes("Kevin")); // true
console.log(squad.includes("Kamau")); // false
```

---

## 3. The Big 4 Modern Array Methods (`.map`, `.filter`, `.find`, `.reduce`) 🚀

Hapa ndipo modern JavaScript inapoacha kutumia zile `for` loops za kizamani. Hizi methods nne (`.map`, `.filter`, `.find`, na `.reduce`) ndizo utakazotumia kila siku kazini:

### a) `.map()` — Kubadilisha Kila Item (Transform)
`.map()` inapita kwa kila item ndani ya array, inafanya operation fulani unayotaka, halafu **inatengeneza array mpya kabisa** bila kuharibu ile array ya mwanzo (no mutation):

```javascript
const beiZaMwanzo = [100, 200, 500, 1000];

// Tunataka kuongeza 16% VAT kwa kila bei:
const beiPamojaNaVAT = beiZaMwanzo.map((bei) => {
  return bei * 1.16;
});

console.log(beiPamojaNaVAT); 
// Output: [116, 232, 580, 1160]
```

### b) `.filter()` — Kuchuja Items kwa Condition
`.filter()` inacheck condition kwa kila item. Zile items zinazopata `true` zinabaki, zile za `false` zinatupwa nje:

```javascript
const mpesaTransactions = [50, 1200, 300, 4500, 80, 15000];

// Tunataka kubakisha miamala mikubwa ya Ksh 1,000 na kuendelea pekee:
const miamalaMikubwa = mpesaTransactions.filter((pesa) => {
  return pesa >= 1000;
});

console.log(miamalaMikubwa); 
// Output: [1200, 4500, 15000]
```

### c) `.find()` — Kutafuta Item Moja Maalum
Tofauti na `.filter()` inayoreturn array ya vitu vingi, `.find()` inatafuta na kureturn **ile item ya kwanza kabisa** inayo-satisfy condition yako. Ikipata tu, inatoka:

```javascript
const alamaZaWanafunzi = [45, 58, 82, 91, 64];

// Tafuta mwanafunzi wa kwanza aliyepata A (80 na zaidi):
const firstDistinction = alamaZaWanafunzi.find((alama) => alama >= 80);

console.log(firstDistinction); // Output: 82 (Inarudisha 82 tu, hahangaiki na 91)
```

### d) `.reduce()` — Ku-combine Vitu Vyote Kuwa Single Value
`.reduce()` inachukua array nzima na kuikandamiza (collapse) hadi ibaki namba moja au value moja tu (kama vile jumla ya bill yote ya dukani):

Inachukua vipande viwili: **accumulator** (sanduku linalojaza total) na **currentValue** (item ya sasa):

```javascript
const expenses = [200, 150, 600, 120];

// Tunapiga jumla ya matumizi yote (0 hapo mwishoni ni starting value ya total):
const totalExpenses = expenses.reduce((total, expense) => {
  return total + expense;
}, 0);

console.log(`Total matumizi ya leo ni: Ksh ${totalExpenses}`); 
// Output: Total matumizi ya leo ni: Ksh 1070
```

---

## 4. Array Destructuring & Spread Operator (`...`) ✨

Modern JavaScript ilitupa shortcuts mbili safi sana:

### a) Array Destructuring (Kutoa vitu nje kirahisi)
Badala ya kuandika `const kwanza = array[0]; const pili = array[1];`:

```javascript
const topScores = [98, 85, 76];

const [dhahabu, fedha, shaba] = topScores;

console.log(dhahabu); // 98
console.log(fedha);   // 85
```

### b) Spread Operator (`...`) — Ku-copy na Kuunganisha Arrays
Alama ya nukta tatu (`...`) inaitwa **spread operator**. Inamwaga vitu vya array nje:

```javascript
const majinaA = ["Amina", "Juma"];
const majinaB = ["Otieno", "Wanjiku"];

// Kuunganisha arrays mbili kuwa moja safi:
const squadKamili = [...majinaA, ...majinaB, "Chebet"];
console.log(squadKamili); 
// Output: ["Amina", "Juma", "Otieno", "Wanjiku", "Chebet"]
```

---

## 5. Common Pitfalls with Arrays ⚠️

> [!WARNING] **1. Ku-access Index Isiyokuwepo**
> Kama array ina items 3, index zake ni `0, 1, 2`. Ukijaribu ku-access `array[3]`, JavaScript haitakupa error—itakupa **`undefined`** kimya kimya, na hii inaweza kuleta bugs mbele kwa code!

> [!NOTE] **2. Kusahau ku-return ndani ya `.map()`**
> ```javascript
> const numbers = [1, 2, 3];
> const doubled = numbers.map((n) => {
>   n * 2; // ❌ Umesahau neno 'return'!
> });
> console.log(doubled); // Output: [undefined, undefined, undefined]
> ```
> Kila mara kumbuka ku-return value ndani ya `.map()`, au utumie concise one-liner: `numbers.map(n => n * 2)`.

---

## 6. Practice Exercises 🎯

Fungua console yako (`F12`), jaribu hizi challenges:

1. Tunga array inaitwa `cartPrices` yenye bei za bidhaa 4 (kwa mfano: `[250, 800, 150, 1200]`).
2. Tumia **`.filter()`** kubakisha bidhaa zile zenye bei ni kubwa kuliko Ksh 500 pekee.
3. Tumia **`.map()`** kupea kila bidhaa discount ya 10% (maana yake unazidisha kila bei na `0.9`).
4. Tumia **`.reduce()`** kupiga total amount ya pesa zote zilizobaki kwa cart.

---

**Next topic 👉: [Topic 6: Objects & JSON kwa JavaScript](./06_objects_na_json.md)**
