# Topic 9: DOM Manipulation & Events kwa JavaScript

Hongera kwa kufika somo la tisa na la mwisho kabisa la kozi yetu! 🎉

Hadi sasa, code zetu zote zimekuwa zikifanya kazi ndani ya terminal au browser developer console. Lakini watu wa kawaida hawatumii developer console—wanatumia websites zenye buttons, forms, picha, na maandishi.

Hapo ndipo **DOM Manipulation & Events** zinapoingia. Hapa ndipo JavaScript inapogeuka kuwa remote control ya kuendesha HTML na CSS ya ukurasa wako bila kubonyeza refresh!

---

## 1. DOM ni Nini Hasa? (Document Object Model) 🌳

Unapofungua ukurasa wa website, browser inasoma ule msimbo wa HTML na kuugeuza kuwa muundo wa vitu (tree of objects) ndani ya kumbukumbu ya kompyuta. Huo muundo unaitwa **DOM**.

Kupitia kitu maalum kinachoitwa **`document`**, JavaScript inapata mamlaka kamili ya:
* Kusoma maandishi yoyote kwenye ukurasa.
* Kubadilisha rangi, fonts, na CSS styles.
* Kufuta elements au kuongeza elements mpya za HTML kwa sekunde moja.
* Kusikiliza vitendo vya mtumiaji (kama clicks, typing, au scrolling).

---

## 2. Selecting Elements (Kuchagua Vitu Kwenye Ukurasa) 🎯

Kabla ya kubadilisha kitu, lazima kwanza ukichague. Modern JavaScript inatumia methods mbili kuu zenye nguvu ambazo zinatumia CSS selectors zile zile ulizoea:

### a) `document.querySelector("selector")`
Inachagua **element ya kwanza kabisa** inayo-match selector hiyo (iwe ni `#id`, `.class`, au tag name):

```javascript
// Kuchagua kwa ID:
const title = document.querySelector("#main-heading");

// Kuchagua kwa Class:
const subTitle = document.querySelector(".sub-title");

// Kuchagua kwa Tag name:
const button = document.querySelector("button");
```

### b) `document.querySelectorAll("selector")`
Inachagua **elements zote** zinazoshiriki hiyo class na kuziweka kwenye list (NodeList):

```javascript
const allCards = document.querySelectorAll(".card");
console.log(`Kuna kadi ${allCards.length} kwenye ukurasa!`);
```

---

## 3. Modifying Elements (Kubadilisha Maandishi na Muonekano) 🎨

Ukishashika element mkononi mwako, unaweza kuifanyia mambo kadhaa:

### a) Kubadilisha Maandishi: `textContent` vs `innerHTML`
* **`textContent`**: Inabadilisha maandishi ya kawaida pekee (salama zaidi dhidi ya wadukuzi):
  ```javascript
  title.textContent = "Karibu Nairobi Tech Hub!";
  ```
* **`innerHTML`**: Inakuruhusu kuingiza tags mpya za HTML ndani ya hiyo element:
  ```javascript
  const container = document.querySelector("#box");
  container.innerHTML = "<p>Hii ni paragraph mpya iliyoundwa na <strong>JS!</strong></p>";
  ```

### b) Kubadilisha Styles & Classes (`classList`)
Badala ya kuandika inline styles kwa mkono (`element.style.color = "red"`), njia bora na ya kisasa ni kuongeza au kuondoa CSS classes kwa kutumia **`classList`**:

```javascript
const banner = document.querySelector(".banner");

banner.classList.add("active");       // Inaongeza class ya 'active'
banner.classList.remove("hidden");    // Inatoa class ya 'hidden'
banner.classList.toggle("dark-mode"); // Kama ipo inaitoa, kama haipo inaiweka!
```

---

## 4. Handling Events (Kusikiliza Vitendo vya User) ⚡

**Event** ni kitu chochote kinachofanyika kwenye ukurasa:
* User ku-click button (`click`).
* User ku-type kwenye input box (`input` au `change`).
* User ku-submit form (`submit`).

Tunatumia method inayoitwa **`addEventListener("event", callbackFunction)`**:

### Mfano 1: Click Event
```javascript
const myButton = document.querySelector("#alert-btn");

myButton.addEventListener("click", () => {
  console.log("Button imebonyezwa safi kabisa! 🚀");
});
```

### Mfano 2: Kusoma Maandishi Kutoka kwa Input Field
```javascript
const inputName = document.querySelector("#user-name-input");
const greetingText = document.querySelector("#greeting");

inputName.addEventListener("input", (e) => {
  // e.target.value ndiyo ile value user anayotype kwa muda huo:
  greetingText.textContent = `Niaje ${e.target.value}!`;
});
```

---

## 5. Mfano Kamili wa Pamoja: Mini Interactive App 💡

Huu hapa ni mfano kamili unaochanganya HTML na JavaScript:

```html
<!-- HTML Structure -->
<div class="counter-container">
  <h2>Score: <span id="score">0</span></h2>
  <button id="add-btn">+ Ongeza Alama</button>
  <button id="reset-btn">Reset</button>
</div>

<script>
  // JavaScript Logic:
  let count = 0;
  
  const scoreDisplay = document.querySelector("#score");
  const addBtn = document.querySelector("#add-btn");
  const resetBtn = document.querySelector("#reset-btn");

  // Ongeza score wakati addBtn inapofinywa:
  addBtn.addEventListener("click", () => {
    count++;
    scoreDisplay.textContent = count;
  });

  // Rudisha score kuwa zero:
  resetBtn.addEventListener("click", () => {
    count = 0;
    scoreDisplay.textContent = count;
  });
</script>
```

---

## 6. Common Pitfalls kwa DOM ⚠️

> [!WARNING] **1. Ku-run JavaScript kabla ya HTML ku-load**
> Ukijaribu kuita `document.querySelector("#btn")` lakini tag ya `<script>` iko juu kabisa kwenye `<head>` ya HTML yako, JavaScript itarudisha **`null`** kwa sababu browser bado haijafika huko chini kutengeneza hiyo button!
> **Suluhisho**: Weka tag yako ya `<script>` pale chini kabisa kabla ya kufunga `</body>`, au utumie `<script defer src="app.js"></script>`.

> [!NOTE] **2. Kusahau `e.preventDefault()` kwenye Form Submissions**
> Forms kwa asili huwa na tabia ya kurefresh ukurasa mzima zikisubmitiwa. Ili kuzuia hiyo tabia na kuruhusu JavaScript ishike data:
> ```javascript
> form.addEventListener("submit", (e) => {
>   e.preventDefault(); // Inazuia browser ku-reload ukurasa!
>   // Sasa tuma data kwa API...
> });
> ```

---

## 7. Quick Practice 🎯

1. Tengeneza button kwenye ukurasa wa HTML yenye id `#mode-toggle`.
2. Kwa kutumia JavaScript, weka `click` event listener.
3. Kila button hiyo inapofinywa, tumia **`document.body.classList.toggle("dark-theme")`** kubadilisha theme ya website kutoka light kwenda dark mode.
4. Badilisha maandishi ya button hiyo ili yasomeke: *"Switch to Light"* au *"Switch to Dark"* kulingana na theme ya sasa!

---

## 🏁 Hitimisho la Kozi (Course Completion) 🎓

Hongera sana! Ukiwa umekamilisha masomo yote 9 kuanzia `Variables` hadi `DOM Manipulation`, sasa una msingi imara sana wa **Modern JavaScript** ulioandikwa kwa lugha halisi inayoeleweka bila usumbufu wa "deep translation".

Rudi kwenye **[`README.md`](./README.md)** kupitia masomo yote wakati wowote unapotaka kukumbuka concept yoyote!
