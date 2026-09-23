# Module 03: Loops & Iteration

Karibu lesson three! Baada ya kuona logic na venye computer inaexecute decision kwa topic two, sasa ni time ya kuangalia **loops**.

Fikiria situation enye unataka ku-print numbers 1 hadi 100, au ku-send SMS ya notification kwa customers 500 kwa database. Badala ya kuandika `console.log()` mara mia moja (utachoka bure!), unapea computer hiyo kazi by using **loop**.

Loop simply inatell computer: *"Endelea kuexecute hii block ya code tena na tena until condition enye umeeka ikuwe 'falsified'"*

---

## 1. Main Types of Loops 🔄

Kwa JavaScript, kuna aina nne kuu za loops utakazotumia kila siku:
1. **`for` loop** (The Classic — inatumika sana unapojua the number of times ya looping session itatake).
2. **`while` loop** (Inatumika unapojua condition lakini haujui itajirudia mara ngapi).
3. **`do...while` loop** (Inarun angalau mara moja kwanza kabla ya kucheck condition).
4. **`for...of` loop** (Modern and clean — inatumika kuzunguka kwa arrays au list ya vitu moja kwa moja bila stress).

---

## 2. The Classic `for` Loop ⏱️

Hii ndiyo  most popular loop  . Iko na parts tatu na imeseparatiwa na semi colon (`;`):

```javascript
for (initialization; condition; increment) {
  // Code ya kuexecute kila round hapa
}
```

### Mfano kwa Vitendo:
Hapa tunataka kuhesabu kuanzia 1 hadi 5:

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(`Round number: ${i}`);
}
```

### Venye Comp Inavyoendesha Hii Loop:
1. **`let i = 1` (Initialization)**: Hapa ndipo safari inapoanza. Tunadeclare variable ya counter inayoitwa `i` na kuipa value ya kwanza (`1`). Hii inafanyika mara moja tu mwanzoni.
2. **`i <= 5` (Condition)**: Kabla ya kila round, comp ina-check: *"Je, `i` bado ni less au equal to 5?"* Kama ni `true`, code block inarun. Ikiwa `false`, loop inamalizia hapo.
3. **`console.log(...)`**: Inaprint value ya sasa ya `i`.
4. **`i++` (Increment)**: Mwisho wa kila round, `i` inaongezwa 1 (maana ya `i++` ni `i = i + 1`), alafu comp inarudi step 2 kuangalia condition tena.

Output:
```text
Round number: 1
Round number: 2
Round number: 3
Round number: 4
Round number: 5
```

---

## 3. The `while` Loop ⏳

`while` loop inaangalia condition moja tu. kama condition hiyo ni `true`, the loop continues. 

Inafaa sana wakati haujui loop itachukua mara ngapi (kwa mfano ku-wait user aweke password sahihi, au connection ya server ikuwe established):

```javascript
let batteryLevel = 3;

while (batteryLevel > 0) {
  console.log(`Simu bado iko on, battery level: ${batteryLevel}% 🔋`);
  batteryLevel--; // Tunapunguza battery kwa 1 kila loops
}

console.log("Simu imezima! Plug in charger.");
```

### ⚠️ Warning: Infinite Loop (Danger Zone)
Unajua computer haina akili ya kujiongeza. Ukisahau ku-increment au ku-decrement counter ndani ya `while` loop (kwa mfano ukisahau ile `batteryLevel--`), condition itabaki kuwa `true` milele!

Hiyo inaitwa **infinite loop**—browser yako itahung mara moja na itabidi uforce-quit kupitia Task Manager! 💥

---

## 4. The `do...while` Loop 🚪

Tofauti ya `do...while` na `while` ya kawaida ni ndogo lakini muhimu sana:
* `while`: Inacheck mlango kwanza kabla ya kukuacha uingie.
* `do...while`: Inakuacha uingie na ufanye kazi **angalau mara moja**, halafu ndio inacheck kama inafaa kuendelea round ya pili.

```javascript
let count = 10;

do {
  console.log(`Hii itaprint mara moja tu hata kama condition ni uongo! Count ni: ${count}`);
} while (count < 5); // 10 si ndogo kuliko 5, so condition ni false
```

---

## 5. The Modern `for...of` Loop ✨

Ukiwa na list ya vitu (array) kama majina ya wasanii au bei za bidhaa, kuandika ile `for (let i = 0; i < array.length; i++)` ya zamani inachosha.

Modern JavaScript ilituletea **`for...of`**—inasoma list item moja baada ya nyingine kwa lugha safi sana:

```javascript
const wasanii = ["Sauti Sol", "Nyashinski", "Khaligraph", "Mejja"];

for (const msanii of wasanii) {
  console.log(`Playing track ya: ${msanii} 🎶`);
}
```

Output:
```text
Playing track ya: Sauti Sol 🎶
Playing track ya: Nyashinski 🎶
Playing track ya: Khaligraph 🎶
Playing track ya: Mejja 🎶
```

Hakuna haja ya ku-manage index `i`, comp inakushikia kila item mkononi moja kwa moja!

---

## 6. Controlling Loops: `break` and `continue` 🛑⏩

Kuna time ukiwa katikati ya loop unataka kubadilisha tabia ya loop ghafla:

### a) `break` (Kataa Maneno, Toka Nje Mara Moja)
Inavunja na kusimamisha loop papo hapo, hata kama condition bado ilikuwa `true`. Mfano umepata kile ulichokuwa unatafuta:

```javascript
for (let namba = 1; namba <= 10; namba++) {
  if (namba === 6) {
    console.log("Tumepata namba 6! Simamisha kila kitu hapa. 🛑");
    break; // Loop inatoka nje hapa hapa
  }
  console.log(`Checking namba: ${namba}`);
}
```

### b) `continue` (Ruka Hii Round Moja Tu)
Hii haisimamishi loop nzima. Badala yake, inaruka tu round ya sasa na kukimbilia round inayofuata moja kwa moja:

```javascript
for (let ghorofa = 1; ghorofa <= 5; ghorofa++) {
  if (ghorofa === 3) {
    console.log("Ghorofa ya 3 iko under construction, next! 🚧");
    continue; // Inaruka ghorofa ya 3, lakini itaendelea na 4 na 5
  }
  console.log(`Kusafisha ghorofa number: ${ghorofa}`);
}
```

---

## 7. Common Pitfalls with Loops ⚠️

> [!WARNING] **1. The Off-by-One Error**
> Kuweka `<` badala ya `<=` au opposite yake. Kama unataka loop mara 5 kuanzia 0:
> * `for (let i = 0; i < 5; i++)` inarun mara 5 (0, 1, 2, 3, 4).
> * `for (let i = 0; i <= 5; i++)` inarun mara 6 (0, 1, 2, 3, 4, 5)! Kuwa makini na zero-based indexing.

> [!NOTE] **2. Ku-modify loop counter vibaya**
> Kuwa mwangalifu usibadilishe ile variable ya counter (kama `i`) ndani ya mwili wa code ovyo ovyo bila sababu, utajipata na infinite loop bila kutarajia.

---

## 8. Practice Exercises 🎯

Fungua dev console yako (`F12`), piga hizi mazoezi:

1. Tumia `for` loop ku-print multiples of 5 kuanzia 5 hadi 30 (`5, 10, 15, 20, 25, 30`).
2. Tunga array ya mitaa 4 unayoijua (kwa mfano: `["Rongai", "Westlands", "Kibera", "Kilimani"]`), kisha utumie `for...of` loop ku-print kila mtaa ukiandika: *"Niko kwa hood ya [mtaa]"*.
3. Tumia `for` loop inayohesabu 1 hadi 10, lakini ukitumia `continue` kuruka namba 7 isiprintike.

---

**Next topic 👉: [Topic 4: Functions za JavaScript (Declarations, Arrow Functions, na Scope)](./04_functions_za_javascript.md)**
