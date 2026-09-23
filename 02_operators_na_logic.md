# Module 02: Operators & Logic

Karibu lesson two! Baada ya kuona venye tunastore data kwa `variables` previously  in topic one, sasa ni time ya kujua venye tuna-manipulate hizo data, kufanya hesabu, na kupea computer capability ya kuexecute logic with accuracy.

---

## 1. What are Operators? ⚙️

Kwa kifupi sana, **operators** ni zile alama (symbols) maalum unazotumia kwa code kuambia computer ifanye hesabu fulani au ilinganishe vitu mbili.

Kuna three main group ya operators utakutana nazo day to day:
1. **Arithmetic Operators** (za kufanya hesabu).
2. **Comparison Operators** (za kulinganisha kama vitu ni the same ama different).
3. **Logical Operators** (za kuunganisha conditions kwa statement na kuexecute maamuzi).

---

## 2. Arithmetic Operators ➕➖

Hizi ni alama za hesabu zile za kawaida tulizoea shule, pamoja na zingine kadha za code:

| Operator | Kazi Yake | Mfano wa Code | Matokeo (Output) |
| :---: | :--- | :--- | :---: |
| `+` | Kuadd | `20 + 10` | `30` |
| `-` | Kusubtract | `50 - 15` | `35` |
| `*` | Kumultiply | `5 * 4` | `20` |
| `/` | Kudivide | `100 / 4` | `25` |
| `%` | Modulus ( remainder after division) usiconfuse na percentage | `10 % 3` | `1` |
| `**` | Exponentiation (something to the Power) | `2 ** 3` | `8` *(maana yake 2 × 2 × 2)* |

### Hii Modulus (`%`) Inasaidia Nini?
Unajua mara nyingi unataka kujua kama namba ni even au odd, au change imebaki:
```javascript
// Kama namba ikigawanywa kwa 2 inabaki 0, hiyo ni Even number:
console.log(10 % 2); // 0 (Even)
console.log(11 % 2); // 1 (Odd)
```

### ⚠️ Warning: String Concatenation vs Addition
Kama one of the data ni `string`, alama ya `+` haifanyi hesabu instead inaaunganisha maneno pamoja hii ndiyo inaitwa concatenation:

```javascript
console.log(10 + 20);   // 30 (Hapa zote ni numbers)
console.log("10" + 20); // "1020" (Comp inaona string, kwa hivyo inaziunganisha tu!)
console.log("10" - 5);  // 5 (Hapa JS inajifanya mjanja inaconvert string kuwa number juu minus haina kazi kwa words)
```
> **Rule of thumb**: Kila mara hakikisha data zako ni `Number` kabla ya kuadd ndio usijipate na bugs za ajabu kwa calculations.

---

## 3. Comparison Operators 🔍

Hapa ndipo unapoangalia kama vitu vinalingana au other way round.Answer ya comparison operator kila mara hutoka ikiwa **Boolean** (`true` au `false`).

### `===` (Strict Equality) vs `==` (Loose Equality)
Hapa ndio part enye most of the questions kwa interview ya JavaScript hutoka:

* **`===` (Strict Equality)**: Inaangalia kama **value** na **data type** zinalingana 100%. Hii ndiyo unayofaa kutumia **kila mara by default**.
* **`==` (Loose Equality)**: Hii inajaribu ku-force (type coercion) data types zifanane kabla ya kucompare. Inakuwanga na tabia ya kuleta bugs .

```javascript
// Strict Equality (===) - Inarecommend-iwa kila wakati:
console.log(5 === 5);   // true (zote ni number 5)
console.log(5 === "5"); // false! (moja ni number, nyingine ni string)

// Loose Equality (==) - Epuka hii:
console.log(5 == "5");  // true (Comp inaconvert string "5" kuwa number ndio izilinganishe)
console.log(0 == false); // true (Tabia mbaya ya loose equality!)
```

### Operators Zingine za Comparison:
* `!==` (Strict Not Equal): Inaangalia kama two values hazilingani (`5 !== 10` inaleta `true`).
* `>` ( Greater than)
* `<` ( Less than)
* `>=` (greater or equal to)
* `<=` (lesser or equal to)

```javascript
const ticketPrice = 1000;
const moneyAtHand = 1500;

console.log(moneyAtHand >= ticketPrice); // true (Uko na pesa ya kutosha kuingia!)
```

---

## 4. Logical Operators 🧠

Kuna time utataka ku-check conditions zaidi ya moja kwa wakati mmoja ndio code iexecute decision:

### a) `&&` (AND Operator)
Conditions zote **lazima zikuwe `true`** ndio final output ikuwe `true`. Condition moja ikifail then final output ni false:

```javascript
const nikoNaID = true;
const nikoKadi = true;

// Lazima ukuwe na ID NA pia ukuwe Kadi:
const nawezaKuingia = nikoNaID && nikoKadi;
console.log(nawezaKuingia); // true
console.log("Vote wisely mtu yangu! 🗳️");
```

### b) `||` (OR Operator)
Hapa inahitaji **atleast condition moja ikuwe `true`**. Si must conditions zote mbili au multiple conditions  `zikuwefulfilled` ndio final output ikuwe true

```javascript
const nikoNaPesaMpesa = false;
const nikoNaCash = true;

// Kama uko na pesa M-Pesa AU Cash, bado unaweza kulipa fare:
const nawezaKulipa = nikoNaPesaMpesa || nikoNaCash;
console.log(nawezaKulipa); // true
```

### c) `!` (NOT Operator)
Hii inageuza ukweli kuwa uongo, au uongo kuwa ukweli (inageuza switch):
Just like your subconscious inakushow exclamation inashow the unexpected, hivo tu ndiyo tu inamaanisha kwa hii dimension...Scientist had to make the meaning of the exclamation symbol ikuwe negation. 

```javascript
const mvuaInanyesha = false;
console.log(!mvuaInanyesha); // true (Yaani: "Si kweli kwamba mvua inanyesha")
```

### d) `??` (Nullish Coalescing Operator) ✨
Hii ni modern feature poa sana. Inatumika kutoa **fallback value** kama variable ni `null` au `undefined` pekee:

```javascript
let usernameGari; // bado ni undefined
const jinaLaKuonyesha = usernameGari ?? "Mgeni";
console.log(jinaLaKuonyesha); // Output: "Mgeni" (kwa sababu usernameGari haina value bado)
```

---

## 5. Conditionals: `if`, `else if`, and `else` 🚦

Sasa venye tumeelewa logic operators, tunazitumiaje ku-control flow ya program yetu? Tunatumia `if` statements:

```javascript
const accountBalance = 450;
const fareYaMat = 100;

if (accountBalance >= fareYaMat) {
  console.log("Ingia kwa mat, safari ianze! 🚐");
} else if (accountBalance > 0) {
  console.log("Pesa haitoshi mat, itabidi ushuke utembee half way!");
} else {
  console.log("Account iko zero kijana, vaa smart utembee tu.");
}
```

Venye inavyofanya kazi:
1. JavaScript inacheck condition ya kwanza kwa `if (...)`.
2. Kama ni `true`, inarun hiyo code block na inaruka zingine zote zimebaki.
3. Kama ni `false`, inashuka kucheck `else if (...)`.
4. Kama zote zimefail, inamalizia pale kwa `else` (default fallback).

---

## 6. Ternary Operator (Shorthand `if/else`) ⚡

Kama una condition fupi sana yenye inataka tu kuamua kati ya vitu mbili, sio lazima uandike `if / else` ndefu ya five lines. Unatumia **Ternary Operator** (`? :`):

**Structure:**
`condition ? fanyaHiiKamaNiTrue : fanyaHiiKamaNiFalse;`

```javascript
const age = 19;

// Badala ya kuandika if/else ndefu:
const message = age >= 18 ? "Wewe ni mtu mzima" : "Wewe bado ni mtoi, rudi class!!";

console.log(message); // Output: "Wewe ni mtu mzima"
```

---

## 7. Falsy Values in JavaScript ⚠️

Unajua kwa JS, sio lazima variable iwe neno `false` ndio ichukuliwe kama uongo kwa `if` condition. Kuna values 6 maalum zenye zikipigwa kwa `if`, JavaScript inaziona kama `false` mara moja:

1. `false`
2. `0` (nambari zero)
3. `""` (empty string)
4. `null`
5. `undefined`
6. `NaN` (Not a Number)

Vitu vingine vyote (hata empty array `[]` au empty object `{}`) kwa JS ni **truthy**!

```javascript
const emptyString = "";

if (emptyString) {
  console.log("Hii haitaprint kamwe!");
} else {
  console.log("Empty string ni falsy value! ❌");
}
```

---

## 8. Practice Exercises 🎯

Fungua browser console yako (finya ile `F12`) alafu ujaribu hii challenge:

1. Declare variable `fareBalance` ukitumia `let` na uweke `80`.
2. Declare `matatuFare` ukitumia `const` na uweke `100`.
3. Tumia `if/else` ku-check kama `fareBalance >= matatuFare`. Kama ni true, i-print:
   > *"Lipa konda upate receipt."*
   Kama ni false, i-print:
   > *"Konda anasema shuka bana, unakosa Ksh 20!"*
4. Jaribu tena kuandika hiyo logic ukitumia **Ternary Operator** kwa code line moja tu.

---

**Next topic 👉: [Topic 3: Loops & Iteration (`for`, `while`, `for...of`, na `for...in`)](./03_loops_na_mizunguko.md)**
