# React Nested Route App

This project demonstrates how to create a React app with nested routes using `react-router-dom` version 6.

## Prerequisites

- Node.js (version >= 12.0.0)
- Yarn (optional, but recommended)

## Steps to Run the App

1. Clone this repository:

```bash
git clone https://github.com/your-username/nestedroute-app.git
```

2. Install dependencies:

```bash
cd nestedroute-app
yarn install
```

3. Start the development server:

```bash
yarn start
```

Now the app should be running on [http://localhost:3000](http://localhost:3000).

## Steps to Create the Nested Route App

### Step 1

Create a new React app using `create-react-app`:

```bash
yarn create react-app nestedroute-app
```

### Step 2

Install `react-router-dom` version 6:

```bash
yarn add react-router-dom@v6
```

### Step 3

Create a custom route array in the `src/Routes/routes.js` file:

```javascript
// src/Routes/routes.js
import Test1 from "../Components/Test1";
import Test2 from "../Components/Test2";
import Test3 from "../Components/Test3";
import Test4 from "../Components/Test4";
import Test5 from "../Components/Test5";

const CustomRoutes = [
  {
    path: "/hero",
    element: Test3,
    nestedPath: null,
  },
  {
    path: "/test",
    element: Test2,
    nestedPath: [
      {
        path: '/new',
        element: Test4,
        nestedPath: null
      },
      {
        path: '/add',
        element: Test5,
        nestedPath: null
      }
    ],
  },
  {
    path: "/",
    element: Test1,
    nestedPath: null,
  },
];

export default CustomRoutes;
```

### Step 4

Create a no route component in the `src/Components/NoRoute.js` file:

```javascript
// src/Components/NoRoute.js
import React from 'react';

const NoRoute = () => {
  return (
    <>
      please enter a valid route
    </>
  );
};

export default NoRoute;
```

### Step 5

Import the custom routes and the `NoRoute` component in the `src/App.js` file, and set up the routing logic using `Routes` and `Route` components:

```javascript
// src/App.js
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import CustomRoutes from './Routes/routes';
import NoRoute from './Components/NoRoute';

function App() {
  return (
    <Router>
      <Routes>
        {CustomRoutes.map((data, index) => (
          <React.Fragment key={index}>
            <Route path={data.path} element={<data.element />} />

            {data.nestedPath !== null &&
              data.nestedPath.map((nestedData, nestedIndex) => (
                <Route
                  key={nestedIndex}
                  path={`${data.path}${nestedData.path}`}
                  element={<nestedData.element />}
                />
              ))}

            <Route path="*" element={<NoRoute />} />
          </React.Fragment>
        ))}
      </Routes>
    </Router>
  );
}

export default App;
```

That's it! You have now set up a React app with nested routes using `react-router-dom` version 6.
