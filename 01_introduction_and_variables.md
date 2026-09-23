# Module 01: Introduction to JavaScript & Variables

Karibu lesson one! Hapa tutajifunza foundation ya JavaScript, venye code inavyo-run, na venye tunastore data kwa `variables`.

---

## 1. What is JavaScript? 🌐

JavaScript (mara nyingi hufupishwa kama **JS**) ni programming language inayotumika ku-increase interactivity kwa websites. 

Mwaka ni 1995 na hii period JavaScript ilikuwa inatumika kwa browser kufanya vitu kama button clicks, popup messages na animations kadha wa kadha, lakini leo:

* **Frontend**: Inatumika kwa browser zote (Chrome, Safari, Firefox, Edge) na frameworks kama React, Vue, na Next.js.
* **Backend**: Kupitia **Node.js** au **Bun**, JavaScript ina-run kwa server—inatengeneza APIs, inaunganishwa na database (kama PostgreSQL, MongoDB), na kushughulikia user authentication.
* **Mobile Apps**: Frameworks kama React Native zinatumia JS kutengeneza apps za Android na iOS.

---

## 2. Getting Started: First "Hello World" 🚀

Huna haja ya ku-install software yoyote nzito ili kuanza. Browser yako tayari ina JavaScript engine ndani yake:

1. Fungua browser (e.g. Google Chrome).
2. Finya `F12` kwenye keyboard yako (au Right Click popote ukurasa alafu click **Inspect**).
3. Click tab inayoitwa **Console**.
4. Type code hii alafu click `Enter`:

```javascript
console.log("Niaje Kenya! Hii ndio code yangu ya kwanza ya JavaScript.");
```

> **`console.log()` ni nini?**
> Ni function ya JavaScript enye inatumika ku-print au kuonyesha output kwa terminal au developer console (hiyo enye umetoka). Inasaidia sana wakati wa ku-debug ili kuona data yako inafanya nini.

---

## 3. What is a Variable? 📦

Fikiria **variable** kama box enye imelabeliwa (label). Kama boxes zozote, variable inatumika ku-store data kwa memory ya kompyuta ili uweze kuitumia tena kwa kuita kwa code.

Kwa JavaScript, tunatumia maneno matatu ku-declare (hapa simply ni moment enye you become a God na unasema *"let there be"* and pop! A new information is formed ✨) variable:
1. `const`
2. `let`
3. `var` *(ya zamani—we have to avoid kuitumia sasa though si error)*

---

## 4. `const` vs `let` vs `var` (Modern Rules) ⚖️

Hii ndiyo rule rahisi ya kufuata unapoandika modern JavaScript:

| Keyword | Reassignable? (Value inaweza kubadilishwa?) | Block Scoped? | Lini Uitume? |
| :--- | :---: | :---: | :--- |
| **`const`** | ❌ Hapana | ✅ Ndio | **Kila mara (by default)**. Tumia hii kama unajua value haitabadilishwa. |
| **`let`** | ✅ Ndio | ✅ Ndio | Tumia pale tu unajua value ya variable **itabadilika** mbele (kama vile loop counter au score ya game). |
| **`var`** | ✅ Ndio | ❌ Hapana *(function-scoped)* | **Inarecommendiwa usitumie hii kwa sahii**. Ni mfumo wa zamani (kabla ya ES6 2015) wenye tabia ya kuleta bugs kwa sababu ya *hoisting*. |

### Mfano kwa Vitendo:

```javascript
// 1. Kutumia const (Constant - thamani haibadiliki)
const country = "Kenya";
const dateOfBirth = 2000;

// Ukijaribu kuibadilisha, JavaScript itatupa TypeError:
// country = "Uganda"; // ❌ TypeError: Assignment to constant variable.


// 2. Kutumia let (value inaweza kubadilika baadaye)
let pointScored = 10;
console.log("Current Score:", pointScored); // Output: 10

// Mchezaji ameshinda points zingine:
pointScored = 25; 
console.log("Current Score:", pointScored); // Output: 25 (Hii inakubalika kabisa!)
```

---

## 5. Primitive Data Types 🧱

Kila value unayoiweka kwa variable ina (**data type**). JavaScript ina 7 primitive data types:

### a) `String` (Maneno / Maandishi)
Hizi words zinawekwa ndani ya double quotes `""`, single quotes `''`, au backticks ` `` `:

```javascript
const jina = "Amani";
const city = 'Mombasa';

// Template Literal (kutumia backticks) - inakuruhusu kuchanganya variables ndani ya string kirahisi:
const message = `Karibu ${jina}, tunajua unatoka ${city}!`;
console.log(message); 
// Output: Karibu Amani, tunajua unatoka Mombasa!
```

### b) `Number` (Nambari)
Hii ina-include both integers na decimals. Unajua Computer haina macho 👀, so lazima tushughulikie hii issue na the type of data each variable inahold—tuna-anticipate before ndio machine ielewe.

```javascript
const age = 24;
const beiYaKuku = 850.50;
const joto = -4; // Pia namba hasi (negative)
```

### c) `Boolean` (Ukweli au Uongo)
💡 *Fun fact*: Hili neno Boolean lilikuwa coined after mathematician fulani anaitwa **George Boole**.

Ina value mbili tu: `true` (kweli) au `false` (uongo):

```javascript
const niMwanafunzi = true;
const lessonAttended = false;
```

### d) `Undefined`
Hii inamaanisha variable imekuwa declared, lakini bado haijapewa value yoyote:

```javascript
let simu;
console.log(simu); // Output: undefined
```

### e) `Null`
Hii inawakilisha **intentional absence of value**. Yaani wewe kama developer umeamua variable ni empty kwa sasa: Empty Debe 🪣

```javascript
let gariLangu = null; // Sina gari kwa sasa, nitaweka value nikinunua
```

### f) `BigInt` & `Symbol` (Special Types)
* `BigInt`: Inatumika pale namba inapokuwa kubwa kupita kiasi (zaidi ya `2^53 - 1`). Mfano: `const idKubwa = 9007199254740991n;`.
* `Symbol`: Inatumika kutengeneza unique identifiers ambazo haziwezi kuingiliana.

---

## 6. Checking Types: `typeof` Operator 🔍

Kama unataka kujua data type ya variable yoyote, tumia neno `typeof`:

```javascript
console.log(typeof "Nairobi");   // "string"
console.log(typeof 254);         // "number"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof null);        // "object"  <-- Hii ni bug maarufu ya kihistoria ya JS, lakini null ni primitive!
```

---

## 7. Naming Conventions ✍️

Ili code yako iwe safi na inayosomeka kirahisi na developers wengine:

1. **Tumia `camelCase`**: Word ya kwanza inaanza na small letters, maneno yanayofuata yanaanza na capital letters:
   * ✅ `jinaLaMtumiaji`, `pesaKwaAkaunti`, `isLoggedIn`
   * ❌ `jinalamtumiaji`, `pesa_kwa_akaunti` *(hii inatumika zaidi Python)*
2. **Case-Sensitive**: JavaScript inatofautisha capital letters from small letters na kwa hivyo variables zitakuwa different:
   * `umri`, `Umri`, na `UMRI` ni variables tatu tofauti kabisa!
3. **Majina yenye maana**:
   * ✅ `const beiYaBidhaa = 1500;`
   * ❌ `const x = 1500;` *(baada ya wiki moja huwezi kumbuka `x` ilikuwa nini)*

---

## 8. Common Pitfalls ⚠️

> [!WARNING] **1. Ku-reassign `const`**
> ```javascript
> const mjiMkuu = "Nairobi";
> mjiMkuu = "Kisumu"; // ❌ TypeError: Assignment to constant variable.
> ```
> Kama unajua data itabadilika (kama counter au status), tumia `let`.

> [!NOTE] **2. Tofauti kati ya `undefined` na `null`**
> * `undefined`: JavaScript ndiyo inasema: *"Hii variable sijapewa value bado."*
> * `null`: Wewe developer ndiye unasema: *"Najua hii ipo, lakini nimeweka tupu kwa makusudi."*

---

## 9. Practice Exercises 🎯

Jaribu kuandika hizi kwenye browser console yako:

1. Declare variable inaitwa `myName` ukitumia `const` na uipe jina lako.
2. Declare variable inaitwa `moneyAtHand` ukitumia `let` na uipe nambari (mfano: `500`).
3. Badilisha `moneyAtHand` iwe `1000`.
4. Tumia template literal (backticks ` `` `) ku-print sentence kama hii:
   > *"Jina yangu ni [myName] na niko Ksh [moneyAtHand] mbele nyuma, Walai billahi."*

---

**Next topic 👉: [Module 02: Operators & Logic](./02_operators_and_logic.md)**
