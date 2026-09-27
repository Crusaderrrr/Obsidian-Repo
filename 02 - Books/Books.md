---

cssclasses:

- wide-85

---

# Читаю сейчас (`$= dv.pages('"02 - Books"').where(p => p.Название && p.Reading && p.progress < 100).length`)

```dataviewjs
const getBooks = () => dv.pages('"02 - Books/library"').where(p => p.Название && p.Reading && p.progress < 100).sort(p => p.Название);

let books = [];

for (const book of getBooks()) {
    const categories = book.Категории.map(
        c => `<span class="category">${toTitleCase(c)}</span>`
    ).join(" ");
    books.push(`<div class="book">
        <a data-tooltip-position="top" data-href="${book.file.name}" href="${book.file.name}.md" class="internal-link" target="_blank" rel="noopener nofollow"><img src="${book.Обложка}" data-filename="${book.file.name}" /></a>
        <progress value="${book.Progress}" max="100"></progress>
        <div class="categories">${categories}</div>
        <div class="pages">${book.Страниц} стр.</div>
    </div>`);
}

dv.el("div", books.join(""), {cls: "books"});

function toTitleCase(str) {
  return str.slice(0, 1).toUpperCase() + str.slice(1)
}
```

# Прочитанное

```dataviewjs
const bookPages = dv.pages('"02 - Books"').where(p => p.Название && p.Progress >= 100).sort(p => p.Название);

const MAX_BOOK_NAME_LENGTH = 50;
let index = 0;

dv.table(
    ["", "Название", "Автор", "Страниц"],
    bookPages.map(p => {
        const shortName = p.Название.length > MAX_BOOK_NAME_LENGTH  
            ? p.Название.substring(0, MAX_BOOK_NAME_LENGTH) + "..." 
            : p.Название;
        const authors = p.Автор.split(",").map(el => el.trim()).join("<br />");
        return [
            ++index,
            dv.fileLink(p.file.path, false, shortName),
            authors,
            p.Страниц
        ];
    })
);
```

# [[Bookshelf|Все Книги]]

```dataviewjs
const bookPages = dv.pages('"02 - Books"').where(p => p.Название).sort(p => p.Название);

const MAX_BOOK_NAME_LENGTH = 50;
let index = 0;

dv.table(
    ["", "Название", "Автор", "Страниц", "Прогресс"],
    bookPages.map(p => {
        const shortName = p.Название.length > MAX_BOOK_NAME_LENGTH  
            ? p.Название.substring(0, MAX_BOOK_NAME_LENGTH) + "..." 
            : p.Название;
        const authors = p.Автор.split(",").map(el => el.trim()).join("<br />");
        return [
            ++index,
            dv.fileLink(p.file.path, false, shortName),
            authors,
            p.Страниц,
            p.Progress + "%"
        ];
    })
);
```
