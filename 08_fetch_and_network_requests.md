# Module 08: Fetch API & Network Requests

Karibu lesson eight! Kwenye topic seven tuliona venye `async/await` inavyofanya kazi. Sasa ni time ya kutumia hiyo nguvu kuunganisha app yako na ulimwengu wa nje (backend servers, live databases, na third-party APIs kama za M-Pesa au weather services) kwa kutumia **Fetch API**.

Kupitia Fetch API, website yako inaweza kuomba data mpya kutoka kwenye server, au kutuma form ya user bila ukurasa ku-reload wala ku-refresh hata mara moja!

---

## 1. Core HTTP Request Methods 🌐

Unapowasiliana na server yoyote mtandaoni kupitia API, unatumia lugha ya **HTTP**. Kuna vitendo vinne (methods) vikuu unavyoweza kufanya:

| Method | Kazi Yake | Mfano wa Kawaida |
| :---: | :--- | :--- |
| **`GET`** | Kuvuta / Kusoma data kutoka kwa server | Kuleta list ya bidhaa za duka au feed ya posts |
| **`POST`** | Kutuma data mpya kwenye server | Kusign-up user mpya au kutuma muamala wa malipo |
| **`PUT / PATCH`** | Ku-update data iliyopo tayari | Kubadilisha profile picture au password |
| **`DELETE`** | Kufuta data kwenye server | Kufuta post au akaunti |

---

## 2. Performing a GET Request 📥

Wakati unapotumia `fetch()`, kuna hatua mbili za lazima lazima ambazo comp inafanya kabla haijakupa data kamili:

1. **Step 1**: Inapiga simu kwa server na kureturn **Response object** (inayoshikilia status kama `200 OK`, lakini data yenyewe bado haijasomwa).
2. **Step 2**: Unaita **`await response.json()`** ili kusoma na kugeuza ile JSON text kuwa JavaScript object ya kawaida.

### Mfano kwa Vitendo:
Hapa tunavuta data halisi ya user kutoka kwa free public testing API:

```javascript
const getUsers = async () => {
  try {
    console.log("Inatuma request kwa server...");

    // Step 1: Piga request
    const response = await fetch("https://jsonplaceholder.typicode.com/users/1");

    // Step 2: Parse response kuwa JSON
    const user = await response.json();

    console.log("Data imewasili salama! 🎉");
    console.log(`Jina: ${user.name}`);
    console.log(`Email: ${user.email}`);
    console.log(`Mji: ${user.address.city}`);
  } catch (error) {
    console.log("Kumetokea network error:", error.message);
  }
};

getUsers();
```

---

## 3. Understanding HTTP Status Codes 🚦

Server inapokujibu, inakupa nambari ya siri inayoitwa **Status Code** kukuambia kama mambo yameenda poa au yameharibika:

* **`200 OK`**: Kila kitu kimeenda smooth, data yako hii hapa!
* **`201 Created`**: Mara nyingi inatoka baada ya `POST`—inamaanisha record mpya imetengenezwa kwa database.
* **`400 Bad Request`**: Umetuma data yenye makosa (kwa mfano umesahau kuweka password).
* **`401 / 403 Unauthorized / Forbidden`**: Huna ruhusa! Weka login token au ulipe kwanza.
* **`404 Not Found`**: Kitu ulichoomba hakipo kabisa kwa server (kama user mwenye ID haipo).
* **`500 Internal Server Error`**: Backend imechomeka au server ya mwenyewe ime-crash!

### Ku-check kama Request Imefaulu (`response.ok`):
```javascript
const response = await fetch("https://api.huduma.go.ke/data");

// response.ok inakuwa true kama status ni kati ya 200 na 299:
if (!response.ok) {
  throw new Error(`Server imetupa kosa: Status ${response.status}`);
}

const data = await response.json();
```

---

## 4. Performing a POST Request 📤

Unapotaka kutuma data mpya (kwa mfano ku-register account au kutuma order), unampa `fetch` parameter ya pili yenye options tatu muhimu:
1. `method: "POST"`
2. `headers`: Kuambia server kwamba data inayokuja ni ya mtindo wa JSON (`"Content-Type": "application/json"`).
3. `body`: Ile data yenyewe ikiwa imebadilishwa kuwa text string ukitumia **`JSON.stringify()`**.

```javascript
const createNewPost = async () => {
  const newPostData = {
    title: "Niaje Developers wa Kenya!",
    body: "JavaScript bila deep translation inabamba sana.",
    userId: 254
  };

  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(newPostData)
    });

    const savedData = await response.json();
    console.log("Post imehifadhiwa kwa server!", savedData);
  } catch (error) {
    console.log("Error wakati wa kutuma post:", error);
  }
};

createNewPost();
```

---

## 5. Common Pitfalls with Fetch API ⚠️

> [!WARNING] **1. Kufikiri HTTP 404 au 500 inakimbilia kwa `catch` block**
> Hili ndilo kosa namba moja la developers:
> `fetch()` haitupi error (haireject) ikiwa server imerudisha `404 Not Found` au `500 Server Error`. Inareject pale tu internet inapokatika kabisa (network failure)!
> Kwa hivyo, **kila mara tumia `if (!response.ok)`** kuangalia kama kuna tatizo la HTTP kabla ya kuendelea.

> [!NOTE] **2. Kusahau `await` kwenye `response.json()`**
> ```javascript
> const res = await fetch(url);
> const data = res.json(); // ❌ Umesahau 'await' hapa!
> console.log(data); // Inaprint: Promise { <pending> }
> ```
> `response.json()` yenyewe pia ni Promise, kwa hivyo lazima iwe na `await`.

---

## 6. Practice Exercises 🎯

Fungua console yako (`F12`), fanya hii challenge:

1. Tumia `fetch()` na `async/await` ku-vuta data ya post ya kwanza kutoka:
   `https://jsonplaceholder.typicode.com/posts/1`
2. Cheki kama `response.ok` ni true. Kama si true, tupa error.
3. Parse ile data kwa `await response.json()`, halafu u-print:
   > *"Title ya Post: [title]"*
   > *"Content: [body]"*
4. Jaribu kuweka URL yenye makosa makusudi (kwa mfano `posts/999999`) uone venye error inashikwa kwa `try...catch`.

---

**Next topic 👉: [Module 09: DOM Manipulation & Events](./09_dom_manipulation_and_events.md)**
