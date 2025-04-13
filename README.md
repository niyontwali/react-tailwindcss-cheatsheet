## 🧠 React - Tailwindcss Cheat Sheet

---

**Note**: This assumes you're working inside a Vite + React project and are following best practices such as:
- Using **arrow functions** for defining components and handlers
- Keeping **functions outside of JSX** where possible for clarity and reusability

---

### 1. **JSX (JavaScript XML)**
JSX lets you write HTML in JavaScript. It's syntactic sugar for `React.createElement()`.
```jsx
const Welcome = () => {
  return (
    <div>
      <h1>Hello, world!</h1>
    </div>
  );
};
```
- All tags must be closed.
- Use `className` instead of `class`.

---

### 2. **useState Hook**
Manages local state inside a functional component.
```jsx
import { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => setCount(count + 1);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};
```

---

### 3. **useEffect Hook**
Performs side effects in a component (e.g., fetching data, timers).
```jsx
import { useEffect, useState } from 'react';

const fetchData = async (setData) => {
  const res = await fetch('https://api.example.com/data');
  const json = await res.json();
  setData(json);
};

const DataFetcher = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetchData(setData);
  }, []);

  return (
    <div>
      {data ? <p>{data.message}</p> : <p>Loading...</p>}
    </div>
  );
};
```

---

### 4. **Props**
Used to pass data from parent to child components.
```jsx
const Greeting = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};

const App = () => {
  return <Greeting name="John" />;
};
```

---

### 5. **Conditional Rendering**
Render elements based on a condition.
```jsx
const Auth = ({ isLoggedIn }) => {
  return (
    <div>
      {isLoggedIn ? <p>Welcome back!</p> : <p>Please log in.</p>}
    </div>
  );
};
```

---

### 6. **Handling Forms**
Control input values with state.
```jsx
import { useState } from 'react';

const ContactForm = () => {
  const [email, setEmail] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Submitted: ${email}`);
  };

  return (
    <form onSubmit={handleSubmit} className="flex flex-col gap-2">
      <input
        className="border p-2 rounded"
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <button type="submit" className="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700">
        Send
      </button>
    </form>
  );
};
```

---

### 7. **Rendering Lists with Keys**
```jsx
const ItemList = () => {
  const items = ['Apple', 'Banana', 'Cherry'];

  return (
    <ul className="list-disc pl-5">
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
};
```

---

### 8. **useRef Hook**
Access DOM elements directly.
```jsx
import { useRef } from 'react';

const FocusInput = () => {
  const inputRef = useRef();

  const handleClick = () => {
    inputRef.current.focus();
  };

  return (
    <div className="flex flex-col gap-2">
      <input ref={inputRef} type="text" className="border p-2 rounded" />
      <button onClick={handleClick} className="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700">
        Focus Input
      </button>
    </div>
  );
};
```

---

### 9. **Context API**
Pass global data without prop drilling.
```jsx
import { createContext, useContext } from 'react';

const ThemeContext = createContext('light');

const ThemedComponent = () => {
  const theme = useContext(ThemeContext);
  return <div className={`p-4 ${theme === 'dark' ? 'bg-gray-800 text-white' : 'bg-white text-black'}`}>
    The current theme is {theme}
  </div>;
};

const App = () => {
  return (
    <ThemeContext.Provider value="dark">
      <ThemedComponent />
    </ThemeContext.Provider>
  );
};
```

---

### 10. **React Router Basics**
```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

const Home = () => {
  return <h2>Home</h2>;
};

const About = () => {
  return <h2>About</h2>;
};

const App = () => {
  return (
    <BrowserRouter>
      <nav className="flex gap-4 p-4 bg-gray-100">
        <Link to="/" className="text-blue-500 hover:underline">Home</Link>
        <Link to="/about" className="text-blue-500 hover:underline">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
};
```

---

## 🎨 Tailwind CSS Cheat Sheet – Essential Utilities (With Explanations)

### 📦 Layout
| Utility         | Explanation                         |
|----------------|--------------------------------------|
| `flex`, `grid` | Use for layout systems               |
| `flex-col`     | Stack children vertically            |
| `justify-center` | Horizontally center items           |
| `items-center` | Vertically center items              |
| `gap-4`        | Add space between flex/grid items    |

---

### 📐 Spacing (Margin & Padding)
| Utility         | Explanation                         |
|-----------------|--------------------------------------|
| `m-4`, `p-4`     | Margin/Padding on all sides (1rem)  |
| `mt-2`, `mb-4`   | Margin top/bottom only              |
| `px-6`, `py-2`   | Padding x/y direction               |

---

### 🎯 Sizing & Width
| Utility      | Explanation                          |
|--------------|---------------------------------------|
| `w-full`     | Full width of parent                  |
| `w-1/2`      | 50% width                             |
| `h-screen`   | Full height of the viewport           |

---

### 🎨 Color Utilities
| Utility         | Explanation                         |
|-----------------|--------------------------------------|
| `bg-blue-500`   | Background color                    |
| `text-white`    | White text                         |
| `hover:bg-blue-700` | Changes on hover               |

---

### 🔠 Typography
| Utility         | Explanation                          |
|-----------------|---------------------------------------|
| `text-sm`, `text-2xl` | Font size                      |
| `font-bold`, `font-light` | Font weight               |
| `text-center`, `text-left` | Text alignment            |

---

### 🖼️ Border & Radius
| Utility         | Explanation                          |
|-----------------|---------------------------------------|
| `border`        | Adds default border                  |
| `border-2`, `border-t` | Thickness and side control   |
| `rounded`, `rounded-xl` | Border-radius values        |

---

### 🧭 Positioning & Layering
| Utility         | Explanation                          |
|-----------------|---------------------------------------|
| `relative`, `absolute` | Control positioning context   |
| `top-0`, `left-0`      | Position offsets               |
| `z-10`, `z-50`         | Stack order                    |

---

### 📱 Responsive Design (Mobile-first)
| Prefix       | Screen Size       |
|--------------|-------------------|
| `sm:`        | ≥ 640px            |
| `md:`        | ≥ 768px            |
| `lg:`        | ≥ 1024px           |
| `xl:`        | ≥ 1280px           |
| `2xl:`       | ≥ 1536px           |

**Example**:
```html
<div className="text-sm md:text-lg lg:text-xl">
  Responsive Text
</div>
```
This makes the text:
- small by default
- large on medium screens
- extra large on large screens

