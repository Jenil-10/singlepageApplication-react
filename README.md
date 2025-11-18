# singlepageApplication-react
```
React SPA with Protected Dashboard and Nested Routes
This project is a Single Page Application (SPA) built using React Router v6. It includes a Home page, Login page, and a protected Dashboard with nested pages (Profile, Settings, Notifications). The UI matches the layout shown in the final output screenshots, with a clean minimal design and inline navigation links.

Features

SPA using React Router

Protected routes using authentication context

Nested Dashboard pages

Simple login/logout

Clean UI matching final output

Folder Structure
src/
│── components/
│ └── ProtectedRoute.js
│── context/
│ └── AuthContext.js
│── pages/
│ ├── Home.js
│ ├── Login.js
│ ├── Dashboard.js
│ ├── Profile.js
│ ├── Settings.js
│ └── Notifications.js
│── App.js
└── index.js

Installation
npm install
npm start

AuthContext.js

import { createContext, useContext, useState } from "react";

const AuthContext = createContext();

export const AuthProvider = ({ children }) => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  const login = () => setIsAuthenticated(true);
  const logout = () => setIsAuthenticated(false);

  return (
    <AuthContext.Provider value={{ isAuthenticated, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => useContext(AuthContext);


ProtectedRoute.js

import { Navigate } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

const ProtectedRoute = ({ children }) => {
  const { isAuthenticated } = useAuth();
  return isAuthenticated ? children : <Navigate to="/login" />;
};

export default ProtectedRoute;


App.js

import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import Login from "./pages/Login";
import Dashboard from "./pages/Dashboard";
import Profile from "./pages/Profile";
import Settings from "./pages/Settings";
import Notifications from "./pages/Notifications";
import ProtectedRoute from "./components/ProtectedRoute";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/login" element={<Login />} />

        <Route
          path="/dashboard"
          element={
            <ProtectedRoute>
              <Dashboard />
            </ProtectedRoute>
          }
        >
          <Route path="profile" element={<Profile />} />
          <Route path="settings" element={<Settings />} />
          <Route path="notifications" element={<Notifications />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}

export default App;


Dashboard.js

import { Link, Outlet } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

const Dashboard = () => {
  const { logout } = useAuth();

  return (
    <div style={{ padding: "40px" }}>
      <h1 style={{ fontSize: "48px", fontWeight: "900", color: "#1e293b" }}>Dashboard</h1>

      <div style={{ marginBottom: "25px", fontSize: "20px" }}>
        <Link to="profile">Profile</Link> |{" "}
        <Link to="settings">Settings</Link> |{" "}
        <Link to="notifications">Notifications</Link> |{" "}
        <button
          onClick={logout}
          style={{
            padding: "8px 16px",
            background: "#fff",
            border: "1px solid #e2e8f0",
            borderRadius: "8px",
            cursor: "pointer",
            fontSize: "18px"
          }}
        >
          Logout
        </button>
      </div>

      <Outlet />
    </div>
  );
};

export default Dashboard;


Profile.js

export default function Profile() {
  return <h2 style={{ fontSize: "28px", fontWeight: "700" }}>Profile Page</h2>;
}


Settings.js

export default function Settings() {
  return <h2 style={{ fontSize: "28px", fontWeight: "700" }}>Settings Page</h2>;
}


Notifications.js

export default function Notifications() {
  return <h2 style={{ fontSize: "28px", fontWeight: "700" }}>Notifications Page</h2>;
}


Home.js

import { Link } from "react-router-dom";

export default function Home() {
  return (
    <div style={{ padding: "40px" }}>
      <h1>Home Page</h1>
      <Link to="/login">Go to Login</Link>
    </div>
  );
}


Login.js

import { useAuth } from "../context/AuthContext";
import { useNavigate } from "react-router-dom";

export default function Login() {
  const { login } = useAuth();
  const navigate = useNavigate();

  const handleLogin = () => {
    login();
    navigate("/dashboard/profile");
  };

  return (
    <div style={{ padding: "40px" }}>
      <h1>Login Page</h1>
      <button
        onClick={handleLogin}
        style={{
          padding: "10px 20px",
          fontSize: "18px",
          background: "#2563eb",
          color: "#fff",
          borderRadius: "8px",
          cursor: "pointer"
        }}
      >
        Login
      </button>
    </div>
  );
}


index.js

import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { AuthProvider } from "./context/AuthContext";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <AuthProvider>
    <App />
  </AuthProvider>
);

```
output
<img width="1076" height="668" alt="Screenshot 2025-11-18 161251" src="https://github.com/user-attachments/assets/ec6e5253-febc-4b3d-be81-245deb965a20" />
<img width="870" height="553" alt="Screenshot 2025-11-18 161308" src="https://github.com/user-attachments/assets/02bdc94c-e915-4e05-ac19-3ca0de017e0e" />
<img width="1066" height="624" alt="Screenshot 2025-11-18 161327" src="https://github.com/user-attachments/assets/d4339f0d-a597-4343-a22f-7abc873fb525" />
