
```dataviewjs
let books = [];

for (const book of dv.pages('"02 - Books"').where(p => p.Название).sort(p => p.Название)) {
    const categories = book.Категории.map(c => `<span class="category">${c}</span>`).join(" ");
    books.push(`<div class="book">
        <a data-tooltip-position="top" data-href="${book.file.name}" href="${book.file.name}.md" class="internal-link" target="_blank" rel="noopener nofollow"><img src="${book.Обложка}" data-filename="${book.file.name}" /></a>
        <div class="categories">${categories}</div>
        <div class="pages">${book.Страниц} стр.</div>
    </div>`);
}

dv.el("div", books.join(""), {cls: "books"});
```
