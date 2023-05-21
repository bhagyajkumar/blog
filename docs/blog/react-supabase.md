# Developing with Appwrite in React: A Comprehensive Guide

## Introduction

Are you a frontend developer looking to supercharge your web applications with powerful backend functionalities? Look no further! In this comprehensive guide, we'll explore the world of Appwrite—an impressive backend platform that simplifies development by providing robust features such as authentication, database management, storage, serverless functions, and more. By leveraging Appwrite, you can enhance your React applications with seamless integration of these functionalities.

## Prerequisites

Before we begin, let's ensure you have a solid foundation to follow along with this guide. Here are the prerequisites:

- Basic understanding of React: Familiarity with functional components, states, lifecycle events, context API, and React Router DOM (version 5) will be beneficial.

## Getting Started

Let's kick things off by setting up our development environment and integrating Appwrite with our React project.

1. Create a new React application using `create-react-app` by running the following command in your terminal:

    ```shell
    npx create-react-app myapp
    ```

1. Navigate to the project directory and install the necessary libraries by running the following commands:

    ```shell
    cd myapp

    npm install appwrite

    npm install react-router-dom
    ```

1. Open your project in a code editor and navigate to `src/index.js`. Here, we'll integrate `react-router-dom` into our application. Wrap the `App` component with `BrowserRouter` to enable routing capabilities. Modify the `index.js` file as follows:

    ```javascript
    import React from 'react';
    import ReactDOM from 'react-dom';
    import App from './App';
    import { BrowserRouter } from 'react-router-dom';

    ReactDOM.render(
    <React.StrictMode>
        <BrowserRouter>
        <App />
        </BrowserRouter>
    </React.StrictMode>,
    document.getElementById('root')
    );
    ```

1. Impliment routing in your `App.js` file.

    ```js
    import React from 'react';
    import Login from './pages/Login';
    import Signup from './pages/Signup';
    import "bootstrap/dist/css/bootstrap.min.css";
    import { Routes, Route } from 'react-router-dom';

    const App = () => {
    return (
        <Routes>
        <Route path='/' element={<Home />} />
        <Route path='/login' element={<Login />} />
        <Route path='/signup' element={<Signup />} />
        </Routes>
    );
    };

    ```
    The routing in your App.js file is implemented using the Routes and Route components provided by the react-router-dom library. Here's how it works:
    - The `Routes` component wraps the different routes of your application. It acts as a container for all the route definitions.

    With these initial setup steps completed, we're now ready to dive deeper into integrating Appwrite functionalities into our React application. Let's proceed to the next section of the guide.

    The `src/config/appwrite.js` file is a configuration file used to set up the connection and authentication with the Appwrite backend services in your React application. It utilizes the Client and Account classes from the appwrite package to interact with the Appwrite API.

    Here's a breakdown of the code:

    ```js

    import { Client, Account } from 'appwrite';

    const client = new Client()
        .setEndpoint(process.env.REACT_APP_APPWRITE_ENDPOINT) // Your API Endpoint 
        .setProject(process.env.REACT_APP_APPWRITE_PROJECT_ID); // Your project ID

    const account = new Account(client);

    export { client, account };

    ```


    - The `client` constant is created by instantiating a new Client object. The `setEndpoint` method is called to set the API endpoint URL, which is obtained from the `REACT_APP_APPWRITE_ENDPOINT` environment variable. This variable should be set in your environment configuration (in a file named `.env.local`). You can also hardcode those parameters, pointing to your Appwrite backend server.

    - Each individual route is defined using the `Route` component. It specifies the path for the route and the corresponding component to render.

    - The first `Route` component with `path='/'` and `element={<Home />} `specifies the root path of your application. When the URL matches the root path, it renders the Home component.

    - The second Route component with `path='/login'` and `element={<Login />}` specifies the path for the login page. When the URL matches `'/login'`, it renders the Login component.

    - The third Route component with `path='/signup'` and `element={<Signup />}` specifies the path for the signup page. When the URL matches `'/signup'`, it renders the Signup component.

1. The components I used are below

    <details>
        <summary>Here is the Signup component I used</summary>
        ```js

        import React, { useState } from 'react';
        import { useAuth } from '../AuthContext';

        const Signup = () => {
            const [username, setUsername] = useState('')
            const [email, setEmail] = useState('');
            const [password, setPassword] = useState('');
            const { signup } = useAuth();

            const handleSignup = async (e) => {
                e.preventDefault();

                try {
                    await signup(email, password);
                    // Redirect or perform any necessary action upon successful signup
                } catch (error) {
                    // Handle error
                }
            };

            const customGradient = {
                background: "linear-gradient(to right, rgba(106, 17, 203, 1), rgba(37, 117, 252, 1))"

            }

            return (
                <section className="vh-00" style={customGradient}>
                    <div className="container py-5 h-100">
                        <div className="row d-flex justify-content-center align-items-center h-100">
                            <div className="col-12 col-md-8 col-lg-6 col-xl-5">
                                <div className="card bg-dark text-white" style={{ borderRadius: "1rem" }}>
                                    <div className="card-body p-5 text-center">

                                        <div className="mb-md-5 mt-md-4 pb-5">

                                            <h2 className="fw-bold mb-2 text-uppercase">Signup</h2>
                                            <p className="text-white-50 mb-5">Please enter your details and password!</p>
                                            <form onSubmit={handleSignup}>
                                                <div className="form-outline form-white mb-4">
                                                    <input onChange={(e) => setUsername(e.target.value)} value={username} type="text" id="typeUsernameX" className="form-control form-control-lg" />
                                                    <label className="form-label" htmlFor="typeEmailX">Username</label>
                                                </div>
                                                <div className="form-outline form-white mb-4">
                                                    <input onChange={(e) => setEmail(e.target.value)} value={email} type="email" id="typeEmailX" className="form-control form-control-lg" />
                                                    <label className="form-label" htmlFor="typeEmailX">Email</label>
                                                </div>
                                                <div className="form-outline form-white mb-4">
                                                    <input onChange={(e) => setPassword(e.target.value)} value={password} type="password" id="typePasswordX" className="form-control form-control-lg" />
                                                    <label className="form-label" htmlFor="typePasswordX">Password</label>
                                                </div>
                                                <button className="btn btn-outline-light btn-lg px-5" type="submit">Signup</button>
                                            </form>

                                            <div className="d-flex justify-content-center text-center mt-4 pt-1">
                                                <a href="#!" className="text-white"><i className="fab fa-facebook-f fa-lg"></i></a>
                                                <a href="#!" className="text-white"><i className="fab fa-twitter fa-lg mx-4 px-2"></i></a>
                                                <a href="#!" className="text-white"><i className="fab fa-google fa-lg"></i></a>
                                            </div>

                                        </div>

                                        <div>
                                            <p className="mb-0">Don't have an account? <a href="#!" className="text-white-50 fw-bold">Sign Up</a>
                                            </p>
                                        </div>

                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </section>
            );
        };

        export default Signup;
        ```

    </details>


    <details>
        <summary>Here is the login component I used </summary>
        ```js
        import React, { useState } from 'react';
        import { useAuth } from '../AuthContext';
        import { useNavigate } from 'react-router-dom';

        const Login = () => {
            const navigate = useNavigate()

            const [email, setEmail] = useState('');
            const [password, setPassword] = useState('');
            const { login } = useAuth();

            const handleLogin = async (e) => {
                e.preventDefault();

                try {
                    await login(email, password);
                    navigate("/")
                    // Redirect or perform any necessary action upon successful login
                } catch (error) {
                    // Handle error
                }
            };

            const customGradient = {
                background: "linear-gradient(to right, rgba(106, 17, 203, 1), rgba(37, 117, 252, 1))"

            }

            return (
                <section className="vh-00" style={customGradient}>
                    <div className="container py-5 h-100">
                        <div className="row d-flex justify-content-center align-items-center h-100">
                            <div className="col-12 col-md-8 col-lg-6 col-xl-5">
                                <div className="card bg-dark text-white" style={{ borderRadius: "1rem" }}>
                                    <div className="card-body p-5 text-center">

                                        <div className="mb-md-5 mt-md-4 pb-5">

                                            <h2 className="fw-bold mb-2 text-uppercase">Login</h2>
                                            <p className="text-white-50 mb-5">Please enter your login and password!</p>
                                            <form onSubmit={handleLogin}>

                                                <div className="form-outline form-white mb-4">
                                                    <input onChange={(e) => setEmail(e.target.value)} value={email} type="email" id="typeEmailX" className="form-control form-control-lg" />
                                                    <label className="form-label" htmlFor="typeEmailX">Email</label>
                                                </div>
                                                <div className="form-outline form-white mb-4">
                                                    <input onChange={(e) => setPassword(e.target.value)} value={password} type="password" id="typePasswordX" className="form-control form-control-lg" />
                                                    <label className="form-label" htmlFor="typePasswordX">Password</label>
                                                </div>
                                                <p className="small mb-5 pb-lg-2"><a className="text-white-50" href="#!">Forgot password?</a></p>
                                                <button className="btn btn-outline-light btn-lg px-5" type="submit">Login</button>
                                            </form>

                                            <div className="d-flex justify-content-center text-center mt-4 pt-1">
                                                <a href="#!" className="text-white"><i className="fab fa-facebook-f fa-lg"></i></a>
                                                <a href="#!" className="text-white"><i className="fab fa-twitter fa-lg mx-4 px-2"></i></a>
                                                <a href="#!" className="text-white"><i className="fab fa-google fa-lg"></i></a>
                                            </div>

                                        </div>

                                        <div>
                                            <p className="mb-0">Don't have an account? <a href="#!" className="text-white-50 fw-bold">Sign Up</a>
                                            </p>
                                        </div>

                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </section>
            );
        };

        export default Login;

        ```
        
    </details>

    I have used a custom hook `useAuth` to handle authentication.


## Creating a custom hook to manage authentication.

Create a file `AuthContext.jsx` in your `src/` directory.

Here is the contents of the file.

```js
import React, { createContext, useContext, useEffect, useState } from 'react';
import { account } from './config/appwrite';
import { ID } from 'appwrite';

const AuthContext = createContext();

export const useAuth = () => useContext(AuthContext);

export const AuthProvider = ({ children }) => {
  const [currentUser, setCurrentUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Check if the user is logged in
    account
      .get()
      .then((response) => {
        setCurrentUser(response);
        setLoading(false);
      })
      .catch((error) => {
        setLoading(false);
      });
  }, []);

  const signup = async (email, password) => {
    try {
      const response = await account.create(ID.unique(), email, password);
      setCurrentUser(response);
    } catch (error) {
      alert(error);
    }
  };

  const login = async (email, password) => {
    try {
      const response = await account.createEmailSession(email, password);
      setCurrentUser(response);
    } catch (error) {
      alert(error);
    }
  };

  const logout = async () => {
    try {
      await account.deleteSession('current');
      setCurrentUser(null);
    } catch (error) {
      // Handle error
    }
  };

  const value = {
    currentUser,
    loading,
    signup,
    login,
    logout,
  };

  return (
    <AuthContext.Provider value={value}>
      {!loading && children}
    </AuthContext.Provider>
  );
};

```

- The `AuthContext` is created using the `createContext` function from React. This context will be used to provide authentication-related data and functions to other components in your application.

- The `useAuth` hook is exported, which allows other components to access the values provided by the authentication context.

- The `AuthProvider` component is created to wrap the authentication context around your application. It takes the children prop, which represents the child components that will be rendered inside the `AuthProvider`.

- Inside the `AuthProvider`, the currentUser and loading states are initialized using the useState hook. The `currentUser` state represents the currently logged-in user, while the loading state indicates whether the authentication process is still ongoing.

- The `useEffect` hook is used to check if the user is already logged in. It makes an API call to `account.get()` and updates the `currentUser` state with the response. Once the API call is completed or encounters an error, the `loading` state is set to false.

- The `signup` function is defined to handle the user signup process. It makes an API call to `account.create` with the provided email and password, and upon successful response, updates the `currentUser` state with the created user.

- The `login` function is defined to handle the user login process. It makes an API call to `account.createEmailSession` with the provided email and password, and upon successful response, updates the `currentUser` state with the logged-in user.

- The `logout` function is defined to handle the user logout process. It makes an API call to `account.deleteSession` to delete the current session, and then sets the `currentUser` state to `null`.

## conclusion


Certainly! Here's the conclusion with the mention of the sample repository:

In conclusion, this comprehensive guide has explored the process of working with Appwrite in a React application. We started by setting up the necessary prerequisites, including a basic understanding of React and installing the required libraries.

Next, we covered the implementation of routing in the App.js file, using the react-router-dom library. The routing configuration allowed us to define different routes for different pages and render the corresponding components based on the URL path.

We also examined the implementation of the authentication context in the authContext.js file. This context provided functionality for user authentication, including signup, login, logout, and retrieving the current user's information. The context was wrapped around the application using the AuthProvider component.

Throughout the guide, we explored various code snippets and explained their functionalities, enabling you to understand how Appwrite, React, routing, and authentication can be seamlessly integrated.

To further assist you in your development journey, a sample boilerplate repository has been created as a reference. You can find it at https://github.com/bhagyajkumar/react_appwrite_biolerplate/. The repository provides a starting point with preconfigured settings for working with Appwrite in a React application.

By following this guide and referencing the sample repository, you should now have a solid foundation for developing powerful web applications using Appwrite in a React environment. Feel free to explore more of Appwrite's features and continue building upon the knowledge gained here to create robust and scalable applications.

Happy coding!
