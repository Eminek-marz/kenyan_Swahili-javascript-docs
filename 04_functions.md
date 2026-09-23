# Module 04: Functions

Karibu lesson four! Kufikia sasa tumeshaona variables, logic za ku-make decisions, na loops za kurudia kazi. Sasa ni time ya kuangalia mojawapo ya tools zenye nguvu zaidi kwa programming: **Functions**.

Fikiria function kama mashine maalum ya jikoni au dispenser ya maji. Kazi yake ni kuchukua ingredients au inputs fulani (parameters), kuexecute kazi maalum ndani yake, halafu inakutolea finished product (return value).

Badala ya kuandika code hiyo hiyo yenye mistari ishirini kila mahali kwa project yako, una-pack hiyo logic ndani ya **function** moja. Kuanzia hapo, unaweza ku-call hiyo function mara elfu moja kwa kuandika tu jina lake kwa line moja! Hii ndiyo principle inaitwa **DRY (Don't Repeat Yourself)**.

---

## 1. Function Declarations (The Classic Way) 🏛️

Hii ndiyo njia ya kwanza na ya kitamaduni ya kutengeneza function kwa JavaScript. Inatumia keyword ya `function`:

```javascript
function jinaLaFunction(parameter1, parameter2) {
  // Code ya kuexecute hapa
  return jibu;
}
```

### Mfano kwa Vitendo: Kuhesabu Total Fare
Wacha tutengeneze function ya kupiga hesabu ya fare ya watu kadhaa:

```javascript
// 1. Kutengeneza (Declaring) function:
function pigaHesabuYaFare(watu, fareKwaKichwa) {
  const total = watu * fareKwaKichwa;
  return total;
}

// 2. Kuitumia (Calling / Invoking) function:
const fareYaSquad = pigaHesabuYaFare(4, 150);
console.log(`Total fare ya watu 4 ni: Ksh ${fareYaSquad}`); 
// Output: Total fare ya watu 4 ni: Ksh 600
```

---

## 2. Parameters vs Arguments 🎯

Mara nyingi utaskia developers wakitumia haya maneno mawili, na watu wengi huchanganyikiwa:

* **Parameter**: Ni ile placeholder au jina la variable unayoweka wakati una-define function (kwa mfano `watu` na `fareKwaKichwa` hapo juu).
* **Argument**: Ni ile actual value unayopass wakati unaita (calling) hiyo function (kwa mfano namba `4` na `150`).

### Default Parameters (Kuweka Fallback Value)
Kuna time user au caller anaweza kusahau kupass argument. Badala ya comp kutupa `undefined`, unaweza kuweka default value:

```javascript
function salimiaUser(name = "Kijana") {
  console.log(`Niaje ${name}, karibu kwa platform! 👋`);
}

salimiaUser("Brian"); // Output: Niaje Brian, karibu kwa platform! 👋
salimiaUser();        // Output: Niaje Kijana, karibu kwa platform! 👋 (Hapa imetumia default value)
```

---

## 3. The `return` Statement 🛑

Hii ndiyo part beginners wengi huchanganya:

> **`console.log()`** ina-display tu ujumbe kwa screen au developer console ndio uone na macho. Haisaidii computer kuendelea na hesabu.
> 
> **`return`** inatema (produces) ile final value kutoka kwa function ili iweze ku-hifadhiwa kwa variable au kutumika kwa operations zingine mbele kwa code.

```javascript
function ongezaBilaReturn(a, b) {
  console.log(a + b); // Inaprint tu kwa console
}

function ongezaNaReturn(a, b) {
  return a + b; // Inarudisha value mkononi mwako
}

const result1 = ongezaBilaReturn(5, 5); // Inaprint 10, lakini result1 ni undefined!
const result2 = ongezaNaReturn(5, 5);   // result2 sasa inahold value ya 10!

console.log(result2 * 2); // Output: 20 (Inawezekana juu tulitumia return)
```

> **Warning**: Mara tu computer inapofika kwa neno `return`, function inamalizia hapo hapo na kutoka nje mara moja. Code yoyote iliyoandikwa chini ya `return` ndani ya hiyo function haitawahi kuexecute!

---

## 4. Arrow Functions (`() => {}`) — The Modern Standard ⚡

Kwenye modern JavaScript (ES6+), hii ndiyo syntax maarufu zaidi utakayokutana nayo kila siku kwenye projects za React, Node.js, na tech interviews.

Badala ya kuandika lile neno refu `function`, unatumia mshale wa **fat arrow** (`=>`):

```javascript
// Mfano wa kawaida wa Arrow Function:
const hesabuTax = (pesa) => {
  const tax = pesa * 0.16; // 16% VAT
  return tax;
};

console.log(hesabuTax(1000)); // Output: 160
```

### Concise / One-Liner Arrow Functions:
Kama function yako ina line moja tu ya code na inareturn value moja kwa moja, unaweza kutoa curly braces `{}` na lile neno `return`—comp ina-understand moja kwa moja (implicit return):

```javascript
// One-liner fupi na safi kabisa:
const ongezaKumi = (namba) => namba + 10;

console.log(ongezaKumi(50)); // Output: 60
```

---

## 5. Variable Scope (Global vs Block/Function Scope) 🌐🔒

**Scope** inamaanisha ni wapi variable inaweza kufikiwa au kuonekana kwa code yako.

### a) Global Scope
Variable ikideclariwa nje ya function yoyote, iko kwenye **global scope**. Hii ina maana kila function na kila line ya code kwa hiyo file inaweza kuiona na kuitumia:

```javascript
const appName = "MpesaApp"; // Global variable

function displayApp() {
  console.log(`Running: ${appName}`); // Inaonekana hapa bila shida
}

displayApp();
```

### b) Block / Function Scope
Variable ikideclariwa ndani ya function au ndani ya curly braces `{}` (kwa kutumia `const` au `let`), inaishi ndani ya hiyo box pekee. Nje ya hiyo function, **haipatikani**:

```javascript
function loginUser() {
  const secretToken = "xyz123SecretKey"; // Local variable
  console.log("Login successful!");
}

loginUser();

// Ukijaribu kuita secretToken ukiwa nje:
// console.log(secretToken); // ❌ ReferenceError: secretToken is not defined!
```

Comp inakuzuia kwa sababu `secretToken` iko scoped ndani ya `loginUser` pekee. Hii inasaidia sana kuprotect data na kuzuia variables za functions tofauti kuingiliana.

---

## 6. Common Pitfalls with Functions ⚠️

> [!WARNING] **1. Kusahau mabano `()` wakati wa ku-call function**
> ```javascript
> function getStatus() {
>   return "Active";
> }
> console.log(getStatus);   // ❌ Inaprint: [Function: getStatus] (Haija-execute!)
> console.log(getStatus()); // ✅ Inaprint: "Active" (Imekuwa executed)
> ```

> [!NOTE] **2. Kusahau ku-return value**
> Kama function haina neno `return`, by default JavaScript inareturn `undefined`. Kama unataka data itoke nje ya function, kumbuka kuweka `return`.

---

## 7. Practice Exercises 🎯

Finya ile `F12` kwa browser yako, fungua console, upige hizi challenges 3:

1. Tengeneza function inaitwa `calculateTotalWithTip` inayochukua parameters mbili: `billAmount` na `tipPercent`. Ifanye calculation ya tip alafu ireturn total amount.
2. Badilisha hiyo function yako ya swali la kwanza iwe modern **Arrow Function (`=>`)**.
3. Tengeneza function inaitwa `chekiHaliYaHewa` inayochukua parameter ya `isRaining`. Kama ni `true`, ireturn: *"Beba mwavuli bro, kuna mvua!"*. Kama ni `false`, ireturn: *"Hali iko safi, toka nje upigwe na jua."*

---

**Next topic 👉: [Module 05: Arrays & Array Methods](./05_arrays_and_methods.md)**
