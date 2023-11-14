# Sudoku-solver

# Neog- Interview Questions: 

## Format:

The interview questions can be asked from anything that has been covered in the camp. The questions will be in three phases:

1. Coding Question- You can be given a question and asked to code that live on any of the known editors. The coding question can be from any ES6 concept, adding a new feature to your existing assignments/projects, etc. 15 mins will be given for coding question.
2. Project/Assignment code walkthrough- We can ask you to open any of the assignments your have submitted and give a code walkthrough of that. 5 mins will be given for code walkthrough.
3. Concept question- JavaScript, performance, web and React JS core concepts can be asked in the interview. 5 mins will be given for concept question.

## Sample Questions for Interview

 Here are some sample questions. Similar kind of questions will be asked in the interview.

1. Given a basic React app. Implement the sort by price and filter with fast delivery using **useReducer**. Link- https://codesandbox.io/s/usereducer-infinity-wars-iwvvo?file=/src/App.js

```javascript
import React, { useReducer } from "react";
import "./styles.css";

// ... (data remains the same)

const reducer = (state, action) => {
  switch (action.type) {
    case "SORT_BY_PRICE":
      if (action.payload === "ASC") {
        return {
          ...state,
          products: state.products.slice().sort((a, b) => a.price - b.price)
        };
      } else if (action.payload === "DESC") {
        return {
          ...state,
          products: state.products.slice().sort((a, b) => b.price - a.price)
        };
      }
      return state;
    case "FILTER_FAST_DELIVERY":
      return {
        ...state,
        products: state.products.filter(product => product.fastDelivery)
      };
    default:
      return state;
  }
};

export default function App() {
  const [state, dispatch] = useReducer(reducer, { products: data });

  return (
    <>
      <div className="App" style={{ display: "flex", flexWrap: "wrap" }}>
        {state.products.map(
          ({
            id,
            name,
            image,
            price,
            productName,
            inStock,
            level,
            fastDelivery
          }) => (
            // ... (existing JSX remains the same)
          )
        )}
      </div>
      <div style={{ marginTop: "20px" }}>
        <button
          onClick={() => dispatch({ type: "SORT_BY_PRICE", payload: "ASC" })}
        >
          Sort by Price (Low to High)
        </button>
        <button
          onClick={() => dispatch({ type: "SORT_BY_PRICE", payload: "DESC" })}
        >
          Sort by Price (High to Low)
        </button>
        <button onClick={() => dispatch({ type: "FILTER_FAST_DELIVERY" })}>
          Filter by Fast Delivery
        </button>
      </div>
    </>
  );
}

```
2. Create a React app with **UserContext** that stores the user's information (name, Pincode and address). Create a **UserData** component that displays the user's name, pincode and address obtained from the **UserContext** using **useContext**. On change of the user name from a dropdown show the relevant name, address and Pincode.

```javascript
import React, { useState, useContext, createContext } from "react";
import "./styles.css";

// UserContext to store user information
const UserContext = createContext();

const userData = {
  Alice: {
    name: "Alice",
    pincode: "12345",
    address: "123 Main St, Wonderland"
  },
  Bob: {
    name: "Bob",
    pincode: "54321",
    address: "456 Elm St, Bobland"
  }
};

const UserData = () => {
  const user = useContext(UserContext);
  return (
    <div>
      <h2>User Information</h2>
      <p>Name: {user.name}</p>
      <p>Pincode: {user.pincode}</p>
      <p>Address: {user.address}</p>
    </div>
  );
};

const App = () => {
  const [selectedUser, setSelectedUser] = useState("Alice");

  const handleUserChange = (e) => {
    setSelectedUser(e.target.value);
  };

  return (
    <div className="App">
      <h1>User Data using Context</h1>
      <select value={selectedUser} onChange={handleUserChange}>
        <option value="Alice">Alice</option>
        <option value="Bob">Bob</option>
      </select>
      <UserContext.Provider value={userData[selectedUser]}>
        <UserData />
      </UserContext.Provider>
    </div>
  );
};

export default App;
```

### E-commerce Application

1. Write code for filter by color using  a checkbox in your e-commerce application. Have 4 colors: red, blue, yellow and green.
2. Add a Buy Now button which will add the item to cart and instantly take you to the cart page.
3. Add an address type radio button while creating/editing a delivery address. Show it as a label.
    
    ![Screenshot 2023-10-14 at 12.57.17 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8fefe6db-2092-435e-905d-5350a0474ea6/6f8e6a1e-1afd-4efd-b953-15a92797ae8e/Screenshot_2023-10-14_at_12.57.17_PM.png)

   ### TypeScript

1. In an email app add a functionality to retrieve a mail from trash and move back to inbox. Do this using TypeScript.
2. In the Bookmarks app, implement a search feature that allows users to search for bookmarks by title or category. Create a search bar component that:
    - Accepts user input for search queries.
    - Filters and displays bookmarks based on the search query.
    - Supports searching by bookmark title and category.
    - Updates the list of displayed bookmarks as the user types in the search bar.
3. Create a new React component named `EditBookmark` that allows users to edit an existing bookmark. This component should:
    - Receive a prop named `bookmark` containing the bookmark object to edit.
    - Display the current title and URL in input fields.
    - Allow users to modify the title and URL.
    - Include a "Save" button to update the bookmark.
    - Use a form to handle the submission of changes.
    -Invoke a callback function onEditBookmark with the updated bookmark object when the "Save" button is clicked.
Given a function. Add Types to it.
```javascript
const products = [
  { type: "book", title: "The Great Gatsby", price: 10 },
  { type: "electronic", name: "Smartphone", price: 500 },
  { type: "clothing", item: "T-shirt", price: 20 },
];

function calculateTotalPrice(products){
  const totalPrice = products.reduce((total, product) => total + product.price, 0);
	console.log(totalPrice)
}
```
Ans:
```javascript
type Book = {
  type: "book";
  title: string;
  price: number;
};

type Electronic = {
  type: "electronic";
  name: string;
  price: number;
};

type Clothing = {
  type: "clothing";
  item: string;
  price: number;
};

type Product = Book | Electronic | Clothing;

const products: Product[] = [
  { type: "book", title: "The Great Gatsby", price: 10 },
  { type: "electronic", name: "Smartphone", price: 500 },
  { type: "clothing", item: "T-shirt", price: 20 },
];

function calculateTotalPrice(products: Product[]): number {
  const totalPrice: number = products.reduce((total, product) => total + product.price, 0);
  console.log(totalPrice);
  return totalPrice;
}

```
### Backend

1. Write an API to update the price of a dish in a restaurant's menu. Make sure to do error handling.
2. Create an API to get the list of restaurants in descending order of their ratings. Make sure to do error handling.
3. Create an API to get the list of restaurants in ascending order of their delivery time duration. Make sure to do error handling.
4. Create an API to get the details of restaurant which has maximum number of menu items. If there are two or more restaurants, then return all those restaurants.
5. Given a data for TV sets write an api to fetch TVs by price.

```javascript
  const tvSets = [
  {
    id: '1',
    brand: 'Samsung',
    model: 'SUHD-1234',
    screenSize: 55,
    displayType: 'QLED',
    resolution: '4K',
    smartTV: true,
    price: 999,
    color: 'Black',
    weight: 25,
    dimensions: {
      width: 48,
      height: 30,
      depth: 5
    }
  },
  {
    id: '2',
    brand: 'LG',
    model: 'OLED-A1',
    screenSize: 65,
    displayType: 'OLED',
    resolution: '4K',
    smartTV: true,
    price: 1499,
    color: 'Silver',
    weight: 30,
    dimensions: {
      width: 57,
      height: 34,
      depth: 4
    }
  },
  {
    id: '3',
    brand: 'Sony',
    model: 'Bravia-X90J',
    screenSize: 75,
    displayType: 'LED',
    resolution: '8K',
    smartTV: true,
    price: 2999,
    color: 'Black',
    weight: 40,
    dimensions: {
      width: 66,
      height: 40,
      depth: 6
    }
  }
];
 ```
Given a screenshot, write the data model for the given Filpkart washing machine page.
https://file.notion.so/f/f/8fefe6db-2092-435e-905d-5350a0474ea6/c65f1743-2090-407c-8308-8362c41bf74c/Screenshot_2023-11-06_at_8.14.02_PM.png?id=59f849bd-c548-45a1-9a98-1cf9aaff6369&table=block&spaceId=8fefe6db-2092-435e-905d-5350a0474ea6&expirationTimestamp=1699927200000&signature=54Wh-r2VjAKgHOQbauhIeQuedH-LRJOeXg_HnrLWisY&downloadName=Screenshot+2023-11-06+at+8.14.02+PM.png

### Testing

1. Description: Write test cases for the `bankAccountReducer`.
    - `bankAccountReducer` manages a state representing bank accounts with their balances and transaction histories.
    - It handles four types of actions: `"DEPOSIT"`, `"WITHDRAW"`, `"TRANSFER"`, and `"VIEW_TRANSACTIONS"`.
    - For the `"DEPOSIT"` action, money is deposited into a bank account, and the balance is updated.
    - For the `"WITHDRAW"` action, money is withdrawn from a bank account, and the balance is updated.
    - For the `"TRANSFER"` action, money is transferred between two bank accounts, updating the balances of both.
    - For the `"VIEW_TRANSACTIONS"` action, the transaction history of a bank account is retrieved.
2. Description: Write test cases for the `flightReservationReducer`.
    - `flightReservationReducer` manages a state representing flight reservations with passenger information, flight details, and payment status.
    - - It handles five types of actions: `"BOOK_FLIGHT"`, `"CANCEL_RESERVATION"`, `"UPDATE_PASSENGER_INFO"`, `"UPDATE_PAYMENT_STATUS"`, and `"SEARCH_FLIGHTS"`.
- For the `"BOOK_FLIGHT"` action, a new flight reservation is created with passenger details and flight information.
- For the `"CANCEL_RESERVATION"` action, a reservation is canceled, and the flight seats are made available.
- For the `"UPDATE_PASSENGER_INFO"` action, passenger information for a reservation is updated.
- For the `"UPDATE_PAYMENT_STATUS"` action, the payment status for a reservation is updated.
- For the `"SEARCH_FLIGHTS"` action, available flights meeting specific criteria are retrieved.
3. Given a function, write test cases for the function **`findCommonNumber`**.
    
    ```jsx
    function findCommonNumber(arr1, arr2) {
    return arr1.find(item => arr2.includes(item));
    }
    
    const array1 = [2, 4, 6, 9, 11];
    const array2 = [5, 7, 9, 10, 12];
    const commonNumber = findCommonNumber(array1, array2);
    ```
    

### Concept Questions:

1. Explain event loops in javaScript.
<p>The event loop is a mechanism used by JavaScript to manage asynchronous tasks. It continuously checks the task queue to see if there are any tasks waiting to be executed. If there are, it adds the tasks to the call stack.</p>
<img src="https://miro.medium.com/v2/resize:fit:1400/format:webp/1*KlrNrmUn1p54g4UlFlvREQ.png" width="50%" height="50%"/>

2. Explain what is closures with the help of code.
<p>A closure is a JavaScript feature that allows inner functions to access the outer scope of a function. Closures help in binding a function to its outer boundary and is created automatically whenever a function is created.</p>
<p>Example</p>

```javascript
function outerFunction() {
  const outerVar = "I'm from the outer function";

  function innerFunction() {
    console.log(outerVar); // Accessing outerVar from the outer function
  }

  // Return the inner function
  return innerFunction;
}

const myClosure = outerFunction(); // myClosure now holds the innerFunction

// Execute the inner function (which still has access to outerVar)
myClosure(); // Outputs: "I'm from the outer function"
```

<div>
In this example:

* outerFunction contains a variable outerVar and an inner function innerFunction.
* innerFunction is returned from outerFunction and assigned to myClosure.
* Even though outerFunction has finished executing, myClosure retains access to outerVar due to the closure. When myClosure is executed, it can still access and use outerVar.
* Closures are powerful as they enable functions to have persistent access to the variables from their containing scope, providing a way to create private variables and maintain state across function calls. This is often used in scenarios like creating private data or implementing higher-order functions in JavaScript.
</div>

3. What are the different promise methods? Explain with the help of code.

<div>Promises in JavaScript have several methods to handle asynchronous operations. The main methods are:

1. Promise.then()
2. Promise.catch()
3. Promise.finally()

Let's explore each method with examples:

1. **Promise.then() :**
The then method is used to handle the fulfillment of a promise (when it's resolved).

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve("Operation completed successfully!");
    } else {
      reject("Operation failed!");
    }
  }, 1000);
});

myPromise.then((result) => {
  console.log(result); // Outputs: Operation completed successfully!
}).catch((error) => {
  console.error(error); // This block won't be executed in this example
});
```

2. **Promise.catch() :**
The catch method is used to handle the rejection of a promise (when it's rejected).

```javascript

const myPromise = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation
  setTimeout(() => {
    const success = false;
    if (success) {
      resolve("Operation completed successfully!");
    } else {
      reject("Operation failed!");
    }
  }, 1000);
});

myPromise.then((result) => {
  console.log(result); // This block won't be executed in this example
}).catch((error) => {
  console.error(error); // Outputs: Operation failed!
});
```

3. **Promise.finally() :**
The finally method is used to specify a function that will be executed when the promise is either fulfilled or rejected.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve("Operation completed successfully!");
    } else {
      reject("Operation failed!");
    }
  }, 1000);
});

myPromise
  .then((result) => {
    console.log(result); // Outputs: Operation completed successfully!
  })
  .catch((error) => {
    console.error(error); // This block won't be executed in this example
  })
  .finally(() => {
    console.log("Finally block executed, regardless of success or failure.");
  });
```
These methods provide a way to handle the various states of a promise: fulfilled (then), rejected (catch), and the final cleanup or additional logic (finally). Using these methods helps in writing more organized and readable asynchronous code.</div>

5. What are some lifecycle methods in React JS?
<ol>
	<li>Mounting - ComponentDidMount</li>
	<li>Updating - ComponentDidUpdate</li>
	<li>Unmounting - ComponentUnMounting</li>
</ol>

6. Explain the working of different hooks in React JS.
<div>
Here are some commonly used React Hooks:

**1. useState Hook:**
Used to add state to functional components.
Returns an array with the current state value and a function to update it.
```jsx
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```
**2. useEffect Hook:**
Adds side effects to functional components.
Invoked after rendering and can perform actions like data fetching, subscriptions, etc.
```jsx
import React, { useState, useEffect } from "react";

function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    // Data fetching logic
    fetch("https://api.example.com/data")
      .then((response) => response.json())
      .then((result) => setData(result))
      .catch((error) => console.error(error));

    // Cleanup function (optional)
    return () => {
      // Cleanup logic (e.g., canceling subscriptions)
    };
  }, []); // Dependency array (empty means it runs once on mount)

  return <div>{data ? <p>Data: {data}</p> : <p>Loading...</p>}</div>;
}
```
**3. useContext Hook:**
Allows functional components to subscribe to React context without introducing a consumer component.
```jsx
import React, { useContext } from "react";
import MyContext from "./MyContext";

function MyComponent() {
  const contextValue = useContext(MyContext);

  return <p>Context Value: {contextValue}</p>;
}
```
**4. useReducer Hook:**
Manages complex state logic by dispatching actions.
Useful for state transitions that depend on the previous state.
```jsx

import React, { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>Increment</button>
      <button onClick={() => dispatch({ type: "decrement" })}>Decrement</button>
    </div>
  );
}
```
**5. useCallback and useMemo Hooks:**
**useCallback:** Memoizes functions to prevent unnecessary re-renders.
**useMemo:** Memoizes the result of a computation to avoid recomputing it on every render.
```jsx

import React, { useState, useCallback, useMemo } from "react";

function MyComponent() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  const doubledCount = useMemo(() => {
    console.log("Computing doubledCount");
    return count * 2;
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <p>Doubled Count: {doubledCount}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```
These hooks provide a powerful and concise way to manage state, side effects, and other aspects of functional components. They enable developers to write more readable and maintainable code in functional components while still leveraging the features traditionally associated with class components.
</div>

7. What is reconciliation in React JS?

<div>Reconciliation is the process by which React updates the Virtual DOM and determines what changes need to be applied to the actual DOM to keep it in sync with the Virtual DOM. It is a key part of React's efficient updating mechanism, ensuring that the UI remains consistent with the application's state.

Here's how the reconciliation process typically works:

**Render Phase:**

<p>When a component's state or props change, React triggers a re-render of the component.
During this phase, React generates a new Virtual DOM tree representing the updated UI based on the changed state or props.</p>
**Reconciliation Phase:**

<p>React compares the new Virtual DOM tree with the previous one generated for the same component.
It performs a tree-diffing algorithm to identify the differences between the two trees.
React identifies which parts of the Virtual DOM have changed, been added, or been removed.</p>

**Update Phase:**

<p>React computes the most efficient way to update the actual DOM based on the differences found in the reconciliation phase.
Instead of re-rendering the entire UI, React aims to update only the specific parts that have changed.
React generates a minimal set of DOM manipulation instructions to update the real DOM.</p>

**Reconciliation Strategies:**

<p>React employs various strategies to optimize reconciliation, such as key-based reconciliation for lists.
The key attribute in React elements helps React identify which items have changed, been added, or been removed in a list.</p>

```jsx
// Example of key-based reconciliation
function MyList({ items }) {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>{item.text}</li>
      ))}
    </ul>
  );
}
```

By using keys, React can efficiently update the list without re-rendering all items.

Reconciliation is a fundamental part of React's declarative approach to building UIs. It ensures that the application's state changes are reflected accurately in the user interface while optimizing performance by minimizing unnecessary updates to the DOM.</div>

8. Write custom hooks.
9. What are some performance optimizing techniques in React JS or web.
10. Explain how the internet works.
