
### HTML
Tytuł strony
```html
<title>Granice lądowe Polski</title>
```
Podłączenie arkusza stylów o nazwie `style.css`
```html
<link rel="stylesheet" href="style.css">
```
Nagłówek
```html
<h1>Granice lądowe Polski</h1>
```
Tabela
```html
<table>
```
Tytuł tabeli
```html
<caption>Granice lądowe Polski</caption>
```
Nagłówki tabeli
```html
  <thead>
    <tr>
      <th>Nazwa państwa</th>
      <th>Długość granicy (km)</th>
    </tr>
  </thead>
```
Definicja sekcji ciała tabeli
```html
<tbody id="table-body">
  </tbody>
```
Definicja kontenera z klasą `additional-info`
```html
<div class="additional-info">
```
Wbudowany kontener
```html
<span></span>
```
Paragraf o długości wszystkich granic lądowych. Wewnątrz `<span>` o id `total-border-length` zostanie umieszczona wartość długości granic, która będzie wstawiana dynamicznie za pomocą JS.
```html
<p>Długość wszystkich granic lądowych: <span id="total-border-length"></span> km</p>
```
Paragraf o najkrótej granicy. Wewnątrz `<span>` o id `shortest-border` zostanie umieszczona nazwa państwa z najkrótszą granicą, która będzie wstawiana dynamicznie za pomocą JS.
```html
<p>Najkrótsza granica Polski: <span id="shortest-border"></span></p>
```
Paragraf o nadłuższej granicy. Wewnątrz `<span>` o id `longest-border` zostanie umieszczona nazwa państwa z nadłuższą granicą, która będzie wstawiana dynamicznie za pomocą JS.
```html
<p>Najdłuższa granica Polski: <span id="longest-border"></span></p>
```
---
### JS
Dodanie funkcji, która uruchomi się po załadowaniu dokumentu HTML
```js
document.addEventListener('DOMContentLoaded', function() {
```
Tablica, która zawiera nazwy państwa i długość granicy z Polską
```js
  const granice = [
    ["Rosja", 210],
    ["Litwa", 104],
    ["Białoruś", 418],
    ["Ukraina", 535],
    ["Słowacja", 541],
    ["Czechy", 796],
    ["Niemcy", 467],
  ];
```
Sortowanie tablicy alfabetycznie według nazw państw<br/>
`a[0].localeCompare(b[0])` porównuje pierwsze elementy w tablicach, czyli nazwy państw
```js
granice.sort((a, b) => a[0].localeCompare(b[0]));
```
`const sortedByNameDesc` deklaruje zmienną sortedByNameDesc, która będzie przechowywać posortowaną tablicę<br/>
`[...granice]` tworzy kopię tablicy granice<br/>
`.sort((a, b) => b[0].localeCompare(a[0]))` sortuje tablicę alfabetycznie malejąco
```js
const sortedByNameDesc = [...granice].sort((a, b) => b[0].localeCompare(a[0])); 
```
Tablica posortowana po długości granicy rosnąco
```js
const sortedByBorderLength = [...granice].sort((a, b) => a[1] - b[1]);
```
Tablica posortowana po długości granicy malejąco
```js
const sortedByBorderLengthDesc = [...sortedByBorderLength].reverse();
```
`tableBody` przechowuje odniesienie do elementu HTML o id `table-body`.
```js
const tableBody = document.getElementById('table-body');
```
`function generateTable(data) {` definicja funkcji, która generuje zawartość tabeli<br/>
`data.forEach(([country, length]) => {` dla każdego elementu tablicy:<br/>
`const row = document.createElement('tr');` tworzy nowy wiersz tabeli<br/>
`row.innerHTML = <td>${country}</td><td>${length}</td>` ustawia zawartość wiersza tabeli - nazwę państwa i długość granicy<br/>
`tableBody.appendChild(row);` dodaje nowy wiersz do ciała tabeli<br/>
```js
  function generateTable(data) {
    data.forEach(([country, length]) => {
      const row = document.createElement('tr');
      row.innerHTML = `<td>${country}</td><td>${length}</td>`;
      tableBody.appendChild(row);
    });
  }
```
Wywołanie funkcji `generateTable` z tablicą `granice` jako argument funkcji
```js
generateTable(granice);
```
Obliczenie sumy długości wszystkich granic na podstawie tablicy `granice`
```js
const totalBorderLength = granice.reduce((acc, [_, length]) => acc + length, 0);
```
Ustawienie zawartości tekstowej elementu o id `total-border-length`
```js
document.getElementById('total-border-length').textContent = totalBorderLength + " km";
```
Obliczenie najkrótszej granicy
```js
const shortestBorder = granice.reduce((min, current) => min[1] < current[1] ? min : current);
```
Ustawienie zawartości tekstowej elementu o id `shortest-border`
```js
document.getElementById('shortest-border').textContent = shortestBorder[0];
```
Obliczenie najdłuższej granicy
```js
const longestBorder = granice.reduce((max, current) => max[1] > current[1] ? max : current);
```
Ustawienie zawartości tekstowej elementu o id `longest-border`
```js
document.getElementById('longest-border').textContent = longestBorder[0];
```