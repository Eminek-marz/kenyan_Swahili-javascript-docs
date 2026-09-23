# Module 06: Objects & JSON

Karibu lesson six! Kwenye lesson five tuliona venye arrays zinashika list ya vitu. Lakini fikiria ukitaka kueleza kitu kimoja kwa undani zaidi—kwa mfano, kueleza taarifa kamili za **User** mmoja (jina lake, nambari ya simu, email, balance ya akaunti, na kama amelipa registration).

Hapo ndipo **Objects** zinapoingia!

Kama array ni list ya shopping, basi **Object** ni kama kitambulisho cha taifa (ID card), passport, au user profile. Inashikilia data kwa mfumo wa **key-value pairs** ndani ya curly braces `{}`.

```javascript
const userProfile = {
  name: "Brian Otieno",
  age: 26,
  city: "Nairobi",
  isVerified: true,
  accountBalance: 4500.50
};
```

Hapa, `name`, `age`, na `city` zinaitwa **keys** (au properties), na `"Brian Otieno"`, `26`, na `"Nairobi"` ndizo **values** zake.

---

## 1. Accessing & Modifying Properties 🔑

Kuna njia mbili kuu za kusoma au kubadilisha data ndani ya object:

### a) Dot Notation (`object.property`)
Hii ndiyo njia rahisi na inayotumika mara nyingi zaidi:

```javascript
console.log(userProfile.name); // "Brian Otieno"
console.log(userProfile.city); // "Nairobi"

// Kubadilisha (Modify) value:
userProfile.age = 27;

// Kuongeza property mpya:
userProfile.phone = "0712345678";

console.log(userProfile.age);   // 27
console.log(userProfile.phone); // "0712345678"
```

### b) Bracket Notation (`object["property"]`)
Inatumika pale ambapo jina la key linatoka kwa variable, au kama key ina nafasi/space:

```javascript
const queryKey = "city";
console.log(userProfile[queryKey]); // "Nairobi"

// Kama key ina space (ingawa inarecommend-iwa kutumia camelCase):
const gari = {
  "plate number": "KDA 123X"
};
console.log(gari["plate number"]); // "KDA 123X" (Hapa dot notation haiwezi kufanya kazi)
```

---

## 2. Methods Inside Objects ⚙️

Wakati function inapowekwa kama value ndani ya object, inaitwa **method**. Inatumika kupea hiyo object uwezo wa kufanya vitendo:

```javascript
const mpesaAccount = {
  owner: "Amina Mohamed",
  balance: 3000,

  // Hii hapa ni method:
  tumaPesa: function(kiasi) {
    if (kiasi <= this.balance) {
      this.balance = this.balance - kiasi;
      console.log(`Umetuma Ksh ${kiasi}. Salio jipya ni Ksh ${this.balance}`);
    } else {
      console.log("Pesa haitoshi kwa akaunti yako! Piga luku uongeze pesa.");
    }
  }
};

mpesaAccount.tumaPesa(1000); 
// Output: Umetuma Ksh 1000. Salio jipya ni Ksh 2000
```
> **Keyword ya `this` ni nini?**
> Neno `this` ndani ya method linamaanisha: *"Mimi hapa (hii object yenyewe)"*. Kwa hivyo `this.balance` inamaanisha balance ya hii hii akaunti ya `mpesaAccount`.

---

## 3. Nested Objects & Optional Chaining (`?.`) 🛡️

Ndani ya object, unaweza kuweka object nyingine (nested object):

```javascript
const customer = {
  id: 101,
  name: "Kevin Kiprop",
  address: {
    mtaa: "Kilimani",
    building: "Greenwood Heights",
    floor: 4
  }
};

console.log(customer.address.mtaa); // "Kilimani"
```

### ⚠️ Hatari Kubwa na Suluhisho la Optional Chaining (`?.`)
Fikiria mteja huyu hajazaza address, kwa hivyo `address` ni `undefined`. Ukijaribu kusema `mteja.address.mtaa`, JavaScript itacrash browser au server yako mara moja na kosa baya la:
`TypeError: Cannot read properties of undefined`!

Ili kujilinda, modern JavaScript ilileta **Optional Chaining (`?.`)**:

```javascript
const mtejaMpya = {
  id: 102,
  name: "Grace Wanjiku"
  // Huyu hana address kabisa!
};

// Badala ya kucrash, inarudisha undefined salama:
console.log(mtejaMpya.address?.mtaa); // undefined (System haicrash!)
```

---

## 4. Object Destructuring & Spread Operator (`...`) ✨

Hizi ni syntax mbili safi sana utakazozitumia kila siku kwenye React na Node.js:

### a) Object Destructuring (Kutoa properties nje bila kuandika maneno mengi)
Badala ya kuandika `const name = user.name; const city = user.city;`:

```javascript
const developer = {
  devName: "Dennis",
  role: "Fullstack Dev",
  level: "Senior"
};

// Destructuring safi kwa line moja:
const { devName, role } = developer;

console.log(devName); // "Dennis"
console.log(role);    // "Fullstack Dev"
```

### b) Spread Operator (`...`) kwa Objects
Inatumika ku-copy object au ku-update property fulani bila kuharibu ile ya mwanzo:

```javascript
const simu = {
  brand: "Samsung",
  model: "S23",
  price: 85000
};

// Tunatengeneza simu mpya kwa ku-copy ya zamani lakini kubadilisha price:
const simuDiscounter = {
  ...simu,
  price: 75000,
  inStock: true
};

console.log(simuDiscounter);
// Output: { brand: "Samsung", model: "S23", price: 75000, inStock: true }
```

---

## 5. What is JSON? (JavaScript Object Notation) 🌐

Unajua wakati app yako inapotaka kuongea na server (backend API au database), huwezi kutuma JavaScript object moja kwa moja kwa waya za internet. Inabidi igeuzwe kuwa **text format** ya kawaida inayoeleweka na kila language (iwe Python, Java, au PHP).

Hiyo text format inaitwa **JSON**.

Kuna methods mbili pekee unazofaa kujua kwa maisha yako kuhusu JSON:

### a) `JSON.stringify(object)`: JS Object ➡️ JSON String
Inachukua JavaScript object yako na kuigeuza kuwa text string ili uweze kuituma kwa API:

```javascript
const userData = { id: 1, username: "kenyanCoder" };

const jsonString = JSON.stringify(userData);
console.log(jsonString); 
// Output: '{"id":1,"username":"kenyanCoder"}' (Hii sasa ni string ya maandishi!)
```

### b) `JSON.parse(string)`: JSON String ➡️ JS Object
Wakati API inapokujibu na text ya JSON, unatumia `JSON.parse()` kuigeuza irudi kuwa JavaScript Object ya kawaida ndio uweze kuisoma na ku-access properties:

```javascript
const responseKutokaServer = '{"status":"success","balance":12500}';

const liveData = JSON.parse(responseKutokaServer);
console.log(liveData.status);  // "success"
console.log(liveData.balance); // 12500 (Sasa unaweza kufanya hesabu nayo!)
```

---

## 6. Common Pitfalls with Objects ⚠️

> [!WARNING] **1. Kulinganisha Objects kwa `===`**
> Unajua comp itafanya nini hapa?
> ```javascript
> const obj1 = { name: "Nairobi" };
> const obj2 = { name: "Nairobi" };
> console.log(obj1 === obj2); // ❌ false!
> ```
> Kwa JavaScript, objects hazilinganishwi kwa contents zao, bali zinalinganishwa kwa **memory address (reference)** zilikohifadhiwa. Kwa sababu `obj1` na `obj2` ni containers mbili tofauti kwa memory, comp inasema hazilingani!

---

## 7. Practice Exercises 🎯

Fungua console yako (`F12`), fanya hizi exercises:

1. Tunga object inaitwa `myLaptop` yenye properties: `brand`, `ram` (e.g. 16), `storage` (e.g. 512), na `isSSD` (boolean `true`).
2. Ongeza property mpya inaitwa `price` kwa kutumia dot notation.
3. Tumia **Object Destructuring** kutoa `brand` na `ram` nje kwa variables huru, kisha uzi-print.
4. Tumia **`JSON.stringify()`** kugeuza `myLaptop` object yako kuwa JSON string, kisha uiprint kwa console uone venye inakaa.

---

**Next topic 👉: [Topic 7: Asynchronous JavaScript & Promises](./07_async_javascript_na_promises.md)**
