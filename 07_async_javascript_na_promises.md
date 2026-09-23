# Module 07: Asynchronous JavaScript & Promises

Karibu lesson seven! Hapa ndipo tunapoingia kwenye mojawapo ya topics zenye nguvu zaidi lakini zinazowasumbua developers wengi: **Asynchronous JavaScript** (mara nyingi inaitwa **Async JS**).

Ukielewa hii topic vizuri, kutengeneza apps zinazowasiliana na backend, databases, na APIs itakuwa rahisi sana kwako.

---

## 1. Synchronous vs Asynchronous Execution ⏳

Kitu cha kwanza unachofaa kujua: **JavaScript ni single-threaded language**. 

Hii ina maana gani? JavaScript ina "mkono" mmoja tu wa kufanya kazi kwa wakati mmoja (iko na Call Stack moja). Haiwezi kufanya kazi mbili za CPU kwa sekunde moja.

### a) Synchronous (Blocking):
Code inarun line by line kuanzia juu kuelekea chini. Kila line lazima isubiri ile ya juu imalize ndio ianze:

```text
Line 1: Inarun... imemaliza.
Line 2: Inarun... (Hii inachukua sekunde 10 ku-download faili kubwa).
Line 3: Imekwama! Haiwezi kuanza hadi Line 2 imalize.
```
> **Shida ya Synchronous**: Kama Line 2 inachukua sekunde 10 ku-fetch data kutoka server ya M-Pesa, browser nzima inafreeze kabisa! User hawezi ku-click button yoyote, hawezi ku-scroll, na ukurasa unakaa kana kwamba kompyuta ime-hang.

### b) Asynchronous (Non-Blocking):
JavaScript inatuma ile task nzito (kama kuomba data kutoka kwa server au kuhesabu sekunde) kando kwenye background, halafu **inaendelea kuexecute code zingine mara moja bila kufreeze ukurasa**. 

Ile kazi nzito ikikamilika kule background, inatuletea majibu.

---

## 2. Simple Async Example: `setTimeout` ⏰

Njia rahisi zaidi ya kuona Async kwa vitendo ni kutumia function ya `setTimeout` (inayohesabu muda kabla ya kuexecute code):

```javascript
console.log("1. Naagiza chakula kwa waiter... 🍽️");

// Hii inachukua sekunde 2 kule background:
setTimeout(() => {
  console.log("2. Chakula kiko tayari mezani! 🍲 (baada ya sekunde 2)");
}, 2000);

console.log("3. Ninaendelea kuongea na marafiki zangu bila kukungoja... 🗣️");
```

### Output:
```text
1. Naagiza chakula kwa waiter... 🍽️
3. Ninaendelea kuongea na marafiki zangu bila kukungoja... 🗣️
2. Chakula kiko tayari mezani! 🍲 (baada ya sekunde 2)
```
> **Angalia vizuri!** Line 3 ime-print kabla ya Line 2! Hiyo ndiyo nguvu ya Asynchronous: JavaScript haikusimama kukungoja sekunde 2 zimalizike—iliendelea na Line 3 kwanza, alafu timer ilipokwisha, ikaleta Line 2.

---

## 3. The Callback Hell Problem 🌀

Zamani sana (kabla ya 2015), developers walikuwa wanatumia callbacks kushughulikia kazi za async. Kama una kazi 4 zinazofuatana (e.g., login user ➡️ pata profile ➡️ pata marafiki zake ➡️ tuma ujumbe), code ilikuwa inakaa hivi:

```javascript
// Hii inaitwa "Callback Hell" au "Pyramid of Doom":
getUser(userId, (user) => {
  getProfile(user, (profile) => {
    getFriends(profile, (friends) => {
      sendMessage(friends[0], () => {
        // Code inazama ndani kama mlima kuelekea kulia!
      });
    });
  });
});
```
Code kama hii ni ngumu kusoma, ngumu ku-debug, na ikitupa error ni kilio!

---

## 4. Handling Async with Promises 🤝

Ili kuokoa developers kutoka kwa Callback Hell, JavaScript ilituletea **Promises**.

Fikiria **Promise** kama receipt au token unayopewa mkahawani ukilipia chakula:
> *"Bado chakula hakijatengenezwa, lakini nakupa hii token kama **ahadi (promise)** kwamba kazi inaendelea. Ikiiva nitakupa chakula chako (**resolved**), na unga ukiisha jikoni nitakupa taarifa kwamba hakuna chakula (**rejected**)."*

Promise inakuwa na states 3 pekee:
1. **`pending`**: Kazi bado inaendelea kwa background.
2. **`fulfilled` (resolved)**: Kazi imefanikiwa, tumepata data!
3. **`rejected`**: Kazi imefeli, kumetokea error (kwa mfano internet imekatika au server imezima).

### Kutumia `.then()` na `.catch()`:
```javascript
// Tuseme hii function inarudisha Promise ya kutuma M-Pesa:
const tumaMpesaPromise = (pesa) => {
  return new Promise((resolve, reject) => {
    const networkIkoSawa = true;

    if (networkIkoSawa) {
      resolve(`Pesa Ksh ${pesa} imetumwa successfully! ✅`);
    } else {
      reject("Network error: Muamala umefeli! ❌");
    }
  });
};

// Kutumia ile Promise:
tumaMpesaPromise(1500)
  .then((jibu) => {
    console.log(jibu); // Inarun kama imefanikiwa (resolve)
  })
  .catch((kosa) => {
    console.log(kosa); // Inarun kama imefeli (reject)
  });
```

---

## 5. Modern Async/Await Syntax 🚀

Ingawa Promises zilikuwa nzuri kuliko Callbacks, kuandika `.then().then().catch()` mara nyingi bado ilikuwa inachosha.

Kwenye ES2017, JavaScript ilituletea **`async` / `await`**. Hii ndiyo syntax inayotumika karibu kila mahali leo. 

Inafanya asynchronous code isomeke kwa uzuri na unadhifu kama synchronous code ya kawaida:

* **`async`**: Inawekwa mbele ya function ili kuashiria kwamba hii function inafanya kazi za asynchronous na inareturn Promise.
* **`await`**: Inaambia computer: *"Tuliza ball hapa kwa hii line, subiri hii Promise imalize na kuleta data ndio usonge mbele!"*

```javascript
// Ku-fetch data ukitumia async/await:
const lipaBili = async () => {
  console.log("Kuanzisha muamala...");

  // Computer inangoja tumaMpesaPromise imalize kabla ya kuendelea:
  const confirmation = await tumaMpesaPromise(2000);
  console.log(confirmation);

  console.log("Muamala umekamilika kabisa!");
};

lipaBili();
```

---

## 6. Error Handling with `try...catch` 🛡️

Wakati unapotumia `async/await`, hautumii tena ile `.catch()`. Badala yake, unatumia mfumo wa kawaida wa **`try...catch`**:

```javascript
const fanyaMuamalaSalama = async () => {
  try {
    console.log("Inatuma maombi kwenye server...");
    const result = await tumaMpesaPromise(5000);
    console.log(result);
  } catch (error) {
    // Kama kuna error yoyote au network ikifeli, inaruka hapa:
    console.log("Okoa jahazi! Error imetokea:", error);
  }
};

fanyaMuamalaSalama();
```

---

## 7. Common Pitfalls with Async JavaScript ⚠️

> [!WARNING] **1. Kusahau neno `await`**
> Unajua comp itafanya nini ukisahau kuweka `await` mbele ya function inayorudisha Promise?
> ```javascript
> const data = tumaMpesaPromise(500); // ❌ Umesahau 'await'!
> console.log(data); // Output: Promise { <pending> }
> ```
> Hautapata ile data uliyotarajia—badala yake utapata object tupu ya Promise ikiwa bado iko `pending`! Kila mara weka `await`.

> [!NOTE] **2. Kutumia `await` bila `async`**
> Neno `await` linaweza kutumika tu ndani ya function iliyowekewa keyword ya `async` mwanzo (isipokuwa kwa top-level modules za kisasa).

---

## 8. Practice Exercises 🎯

Fungua console yako (`F12`), jaribu hii challenge:

1. Tengeneza function inaitwa `fetchUserData` inayorudisha Promise. Ndani yake, tumia `setTimeout` ya sekunde 1 (1000ms) ku-resolve object ya user: `{ id: 1, name: "Brian", role: "Developer" }`.
2. Tengeneza `async function` inaitwa `displayUser`.
3. Ndani ya `displayUser`, tumia **`await`** ku-call ile `fetchUserData`, kisha u-print ujumbe:
   > *"Welcome [name], your role is [role]!"*
4. Weka hiyo logic yote ndani ya block ya **`try...catch`** ili kushika error yoyote ikitokea.

---

**Next topic 👉: [Topic 8: Fetch API & Consuming Network Requests](./08_fetch_api_na_network_requests.md)**
