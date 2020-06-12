# node-sqlite3

### Description
async/await API for making sqlite3 queries in node

### Installation
`npm install a-was/node-sqlite3`

### Usage

```javascript
const SQLite3 = require('node-sqlite3')

async function main() {
    const db = new SQLite3(':memory:')  // or file.sqlite3
    await db.open()  // must open first

    await db.run("CREATE TABLE users (id INT, name TEXT)")
    await db.run("INSERT INTO users (id, name) VALUES (1, 'foo')")

    var rows = await db.all("SELECT id, name FROM users WHERE id = ?", [1])  // params must be iterable
    rows.forEach(row => console.log(row.id, row.name))

    await db.each("SELECT * FROM users", [], function(row) {
        console.log(row)
    })

    await db.close()
}

main()
```
