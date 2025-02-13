# Teknisk Dokumentation for Tema 7 Projekt

## Introduktion
Dokumentation har til formål at gøre projektet og kodebasen mere tilgængelig, så det er nemt for jer at vende tilbage senere eller genbruge kode herfra i nye projekter. Ved at skulle beskrive jeres egen kode, får I en dybere forståelse for, hvordan koden fungerer, og hvorfor bestemte løsninger er valgt. I dette afsnit skal I kort introducere jeres kodebase ved at beskrive jeres tech-stack – hvilke teknologier I har anvendt til at udvikle websitet. Forklar, hvorfor I har valgt disse teknologier, og hvordan de understøtter funktionaliteten i jeres projekt.


## Gruppens aftale omkring navngivning af filer og mapper:
I dette afsnit skal i beslutte hvordan I som gruppe vil navngive filer og mapper for at sikre en ensartet struktur og undgå forvirring.

- Hvordan navngiver vi filnavne? (fx små bogstaver, ingen mellemrum, brug af - eller _)
- Hvordan skal CSS- og JavaScript-filer navngives? (fx base.css og base.js)
- Hvordan sikrer I, at filerne er lette at finde og forstå?

I dette afsnit skal I som gruppe udarbejde en aftale, der sikrer en ensartet navngivning, en klar projektstruktur, der minimerer forvirring og konflikter i Git. Aftalen skal være en rettesnor for alle gruppemedlemmer og sikre, at koden forbliver overskuelig og let at arbejde med.

```
/webprojekt
│── index.html       # Landingpage
└── assets/          # Fx. billeder, fonte, filer brugt på tværs af projektet
    │── base.css     # CSS reset (Boilerplate)
    │── base.js      # JS brugt på tværs af projektet
```

Forklar kort, hvilke formål de enkelte filer har. se ovenstående eksempel:

## Funktionalitet

&#x20;Dette afsnit skal forklare hvad I konkret har arbejde med, for at udvikle websitet. Tænk over hvilke interaktioner brugeren kan foretage på sitet? Eller hvordan  websitet håndterer data? Eksempler på funktionalitet, der kan beskrives:

1. Hentning af produkter fra en API.
2. Filtrering af produkter baseret på brugerens valg.
3. Dynamisk visning af produkter i HTML.

Brug  korte beskrivelser, som i eksemplerne herover

## Dokumentation af Funktion

Her skal I i **fællesskab** finde og beskrive **en** funktion I selv har udviklet. Det kunne eksempelvis være en funktion der generere en listen over produkter:&#x20;

- **Beskrivelse**: Hvad gør funktionen? Hvordan spiller den sammen med resten af koden?
- **Parametre**: Hvilke input forventes (fx en værdi fra en dropdown eller URL'en)?
- **Returnerer**: Beskriv, om funktionen returnerer en værdi eller blot manipulerer DOM’en.
- **Eksempel på brug**: Vis, hvordan funktionen kaldes og anvendes.
- **Implementering**: Inkluder selve kodeeksemplet.

**Implementering:**

```js
const selectedFilter = document.querySelector("#selectFilter");
const productList = document.querySelector("#showProductList");
const products = fetch("https://kea-alt-del.dk/t7/api/products/")
  .then((response) => response.json())
  .then((products) => {
    return products;
  });

function showProducts(event) {
  products.then((products) => {
    let markup = products
      .filter((product) => {
        if (!event) {
          return true;
        } else if (event.target.value == "all") {
          return true;
        } else if (event.target.value == "onSale") {
          return product.discount;
        }
      })
      .map((product) => {
        return /*html*/ `<article
          class="smallProduct ${product.discount && "onSale"} ${
          product.soldout && "soldOut"
        }"
        >
          <img
            src="https://kea-alt-del.dk/t7/images/webp/640/${product.id}.webp"
            alt="product image"
          />
          <h3>${product.productdisplayname}</h3>
          <p class="subtle">${product.articletype} | ${product.brandname}</p>
          <p class="price">DKK <span>${product.price}</span>,-</p>
          <div class="discounted">
            <p>
              Now DKK
              <span
                >${Math.floor(
                  product.price * (1 - product.discount / 100)
                )}</span
              >,-
            </p>
            <p><span>${product.discount}</span>%</p>
          </div>
          <a href="product.html?productId=${product.id}">Read More</a>
        </article>`;
      })
      .join("");
    productList.innerHTML = markup;
  });
}

selectedFilter.addEventListener("change", (event) => {
  console.log(event.target.value);
  showProducts(event);
});

showProducts();
```

## Vigtige takeaways

Hvordan kan denne dokumentation hjælpe jer med at forstå og vende tilbage til projektet senere?&#x20;

Overvej at inkludere: (få hjælp til denne liste med eksempler)

- En kort opsummering af de vigtigste funktioner i projektet.
- Hvordan I kan udvide eller forbedre koden.
- Eventuelle kendte begrænsninger eller forslag til videre arbejde.

Denne struktur sikrer, at dokumentationen er klar, informativ og nem at bruge for jer, hvis I skal vende tilbage til projektet senere eller efterfølgende genbrugt kode i andre projekter.

