# Project Structure as per Scalability in mind.

## Overview of structure

```
/src
  /assets
  /components
  /features
  /hooks
  /layouts
  /pages
  /routes
  /services
  /store
  /styles
  /utils
  /tests
  App.jsx
  index.jsx
```

## Detailed breakdown

1. `/assets`

- **What goes here:** Images, fonts, icons, static files.
- **Best practice:** Keep them organized by type (/images, /icons, /fonts).
- **Problem avoided:** Prevents clutter in components with non-code files.

  Example -

  ```
  /assets
      /images
      logo.png                # Example: company logo
      /icons
      search.svg              # Example: search icon
      /fonts
      Roboto-Regular.ttf      # Example: custom font
  ```

2. `/components`

- **What goes here:** Reusable, generic UI components (buttons, modals, inputs).
- **Best practice:**
  - Use atomic design principles (atoms, molecules, organisms).
  - Keep them dumb (no business logic).
- **Problem avoided:** Prevents duplication and keeps UI consistent.

  Example -
  `components/Button.jsx`

  ```jsx
  export default function Button({ children, onClick, type = "button" }) {
    return (
      <button
        type={type}
        onClick={onClick}
        className="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700"
      >
        {children}
      </button>
    );
  }
  ```

3. `/features`

- **What goes here:** Feature-specific components + logic (e.g., auth, cart, profile).
- **Structure example:**

  Example -

  ```
  /features
      /auth
      AuthForm.jsx            # Example: login/signup form
      authSlice.js            # Example: Redux slice for auth
      authService.js          # Example: API calls for auth
      /cart
      CartItem.jsx            # Example: cart item component
      cartSlice.js            # Example: Redux slice for cart
      cartService.js          # Example: API calls for cart
  ```

- **Problem avoided:** Keeps business logic grouped by domain, not scattered.

4. `/hooks`

- **What goes here:** Custom React hooks (useAuth, useFetch, useDebounce).
- **Best practice:** Prefix with use and keep them reusable.
- **Problem avoided:** Avoids bloated components with repeated logic.

  Example -
  `hooks/useDebounce.js`

  ```jsx
  import { useState, useEffect } from "react";

  export function useDebounce(value, delay = 500) {
    const [debounced, setDebounced] = useState(value);

    useEffect(() => {
      const handler = setTimeout(() => setDebounced(value), delay);
      return () => clearTimeout(handler);
    }, [value, delay]);

    return debounced;
  }
  ```

5. `/layouts`

- **What goes here:** Page layouts (e.g., MainLayout, DashboardLayout).
- **Best practice:** Use layouts to wrap pages with consistent headers/footers.
- **Problem avoided:** Prevents repeating layout code in every page.

  Example -

  ```
  /layouts
      MainLayout.jsx            # Example: header + footer wrapper
      DashboardLayout.jsx       # Example: sidebar + content wrapper
  ```

6. `/pages`

- **What goes here:** Top-level route components (Home, About, Dashboard).
- **Best practice:** Keep them thin—delegate logic to features or hooks.
- **Problem avoided:** Keeps routing clean and pages easy to maintain.

  Example -

  ```
  /pages
      Home.jsx                  # Example: landing page
      About.jsx                 # Example: about us page
      Dashboard.jsx             # Example: user dashboard
  ```

7. `/routes`

- **What goes here:** Centralized route definitions.
- **Best practice:** Define routes in one place, use lazy loading for code splitting.
- **Problem avoided:** Avoids spaghetti routing spread across components.

  Example -
  `routes/AppRoutes.jsx`

  ```jsx
  import { BrowserRouter, Routes, Route } from "react-router-dom";
  import Home from "../pages/Home";
  import About from "../pages/About";
  import Dashboard from "../pages/Dashboard";
  import ProtectedRoute from "./ProtectedRoute";

  export default function AppRoutes() {
    return (
      <BrowserRouter>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route
            path="/dashboard"
            element={
              <ProtectedRoute>
                <Dashboard />
              </ProtectedRoute>
            }
          />
        </Routes>
      </BrowserRouter>
    );
  }
  ```

8. `/services`

- **What goes here:** API calls, backend integrations (REST, GraphQL, Firebase).
- **Best practice:** One service file per domain (authService.js, userService.js).
- **Problem avoided:** Keeps API logic separate from UI.

  Example -
  `services/apiClient.js`

  ```jsx
  import axios from "axios";

  const apiClient = axios.create({
    baseURL: process.env.REACT_APP_API_URL,
    headers: { "Content-Type": "application/json" },
  });

  export default apiClient;
  ```

9. `/store`

- **What goes here:** Global state management (Redux Toolkit, Zustand, Recoil).
- **Best practice:** Organize slices by feature.
- **Problem avoided:** Prevents state chaos and prop drilling.

  Example -

  ```
  /store
      store.js                  # Example: Redux store configuration
      rootReducer.js            # Example: combine all slices
  ```

10. `/styles`

- **What goes here:** Global styles, theme configs, Tailwind/SCSS files.
- **Best practice:** Use a theme system for colors, typography, spacing.
- **Problem avoided:** Prevents inconsistent design.

  Example -

  ```
  /styles
      globals.css               # Example: global CSS
      theme.js                  # Example: theme config (colors, spacing)
  ```

11. `/utils`

- **What goes here:** Helper functions (formatDate, calculateTax, debounce).
- **Best practice:** Keep them pure and reusable.
- **Problem avoided:** Avoids duplicating logic across features.

  Example -

  ```
  /utils
      formatDate.js             # Example: format date helper
      calculateDiscount.js      # Example: discount calculation
      debounce.js               # Example: debounce utility
  ```

12. `/tests`

- **What goes here:** Unit and integration tests.
- **Best practice:** Mirror folder structure of src for easy mapping.
- **Problem avoided:** Keeps tests organized and discoverable.

  Example -

  ```
  /tests
      App.test.js               # Example: test for App component
      utils.test.js             # Example: test for utility functions
  ```
