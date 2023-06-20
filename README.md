# BOOKS APP BLOCKCHAIN

## App to interact with a simple book API to create and fetch books from blockchain via nodejs console

### Setup

```bash
git clone https://github.com/ayush-osmosys/books-app-blockchain
cd books-app-blockchain
```

Now install dependencies

```bash
npm i
```

This would install all the necessary dependencies. Now we will compile the smart contract to create ABI (Application Binary Interfaces) through which we can deploy and interact with the application. To do this, run

```bash
npx hardhat compile
```

After compiling the smart contract, we will deploy it to the blockchain. We will use a test ntework with the help of <code>hardhat</code>. To do this, run

```bash
npx hardhat node
```

This sets up a test network and gives 10 test accounts with credits. **Keep this terminal open.** Now to deploy on this network, open another terminal and run

```bash
npx hardhat run --network localhost scripts/deploy.js
```

You will get an output like

```bash
Deploying contracts with the account:  0xf39Fd6e51aad88F6F4ce6aB8827279cffFb
Account balance:  10000000000000000000000
BookStore address:  0x5FbDB2315678afecb367f032d93F642f64180
```

Copy the address of <code>BookStore</code>. We will use this to refer to our BookStore on the blockchain
This would run the <code>deploy.js</code> script from the <code>scripts</code> folders and deploys the contract on the blockchain network. Now to interact with the contract(i.e add and fetch books from the blockchain network) we will do it in console. To do this, run

```bash
npx hardhat console --network localhost
```

This will open a nodejs REPL terminal. Now we can interact with the contract by first attachinf to our Bookstore using the address we got previously, as

```javascript
const BookStore = await ethers.getContractFactory("BookStore");
```

then

```javascript
const bookStore = await BookStore.attach(
  "0x5FbDB2315678afecb367f032d93F642f64180"
);
```

To add a new book we can run the following command using your bookstore address you got

```javascript
var newBook = { title: "Becoming", year: 2009 };
```

then

```javascript
(await bookStore.addBook(newBook)).toString();
```

Finally lets get all the books by running

```javascript
await bookStore.getBooks();
```
