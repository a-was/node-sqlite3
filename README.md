# node-sqlite3

### Description
async/await API for making sqlite3 queries in node

### Installation
`npm install a-was/node-sqlite3`

### Usage

```javascript
const sqlite3 = require('node-sqlite3')

async function main() {
    // must open db first
    await sqlite3.open(':memory:')  // or file.sqlite3

    await sqlite3.run("CREATE TABLE users (id INT, name TEXT)")
    await sqlite3.run("INSERT INTO users (id, name) VALUES (1, 'foo')")

    var rows = await sqlite3.all("SELECT id, name FROM users WHERE id = ?", [1])
    rows.forEach(row => console.log(row.id, row.name))

    await sqlite3.each("SELECT * FROM users", [], function(row) {
        console.log(row)
    })

    await sqlite3.close()
}

main()
```
