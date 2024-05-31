# Practica-1
trabajo practica, Zahir Rivera
import React, { useState, useEffect } from 'react';
import io from 'socket.io-client';

const Chat = () => {
    const [messages, setMessages] = useState([]);
    const [messageInput, setMessageInput] = useState('');
    const [socket, setSocket] = useState(null);

    useEffect(() => {
        // Conexión al servidor de WebSocket
        const newSocket = io('http://localhost:3001'); // Cambia la URL por la dirección de tu servidor de Socket.IO
        setSocket(newSocket);

        // Manejo de eventos del socket (ejemplo)
        newSocket.on('message', (message) => {
            // Actualizar el estado de los mensajes
            setMessages(prevMessages => [...prevMessages, message]);
        });

        // Limpiar la conexión al desmontar el componente
        return () => {
            newSocket.disconnect();
        };
    }, []);

    const sendMessage = () => {
        // Enviar mensaje al servidor
        socket.emit('sendMessage', messageInput);
        // Limpiar el campo de entrada
        setMessageInput('');
    };

    return (
        <div>
            {/* Renderizar mensajes y formulario de entrada */}
            <ul>
                {messages.map((message, index) => (
                    <li key={index}>{message}</li>
                ))}
            </ul>
            <input type="text" value={messageInput} onChange={(e) => setMessageInput(e.target.value)} />
            <button onClick={sendMessage}>Enviar</button>
        </div>
    );
};

export default Chat;















// src/main.jsx

import React from "react";
import ReactDOM from "react-dom";
import App from "./components/App"; // Importa el componente App
import "./index.css";

// Renderiza el componente App en el elemento con el id "root" en el DOM
ReactDOM.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>,
    document.getElementById("root")
);




















import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

// Utilizamos createRoot en lugar de ReactDOM.render
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>
);


















// /src/components/App.jsx

import Chat from './Chat';

const App = () => {
    return (
        <div>
            <h1>¡Bienvenido a mi aplicación de chat en tiempo real!</h1>
            <Chat />
        </div>
    );
};

export default App;






















import { useState } from 'react';
import firebase from '../services/firebase'; // Importa el objeto firebase configurado

const AuthComponent = () => {
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');

    const handleSignUp = async () => {
        try {
            await firebase.auth().createUserWithEmailAndPassword(email, password);
            // Registro exitoso
        } catch (error) {
            console.error('Error al registrar usuario:', error);
        }
    };

    const handleSignIn = async () => {
        try {
            await firebase.auth().signInWithEmailAndPassword(email, password);
            // Inicio de sesión exitoso
        } catch (error) {
            console.error('Error al iniciar sesión:', error);
        }
    };

    return (
        <div>
            <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} />
            <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} />
            <button onClick={handleSignUp}>Registrarse</button>
            <button onClick={handleSignIn}>Iniciar sesión</button>
        </div>
    );
};

export default AuthComponent;
































import  { useState, useEffect } from 'react';
import io from 'socket.io-client';

const Chat = () => {
    const [messages, setMessages] = useState([]);
    const [messageInput, setMessageInput] = useState('');
    const [socket, setSocket] = useState(null);

    useEffect(() => {
        // Establece la conexión WebSocket
        const newSocket = io('http://localhost:3001'); // Cambia la URL por la dirección de tu servidor de Socket.IO
        setSocket(newSocket);

        // Maneja los eventos de mensajes entrantes
        newSocket.on('message', (message) => {
            // Actualiza el estado con el nuevo mensaje recibido
            setMessages(prevMessages => [...prevMessages, message]);
        });

        // Cierra la conexión al desmontar el componente
        return () => {
            newSocket.disconnect();
        };
    }, []);

    const sendMessage = () => {
        // Envía el mensaje al servidor a través de WebSocket
        socket.emit('sendMessage', messageInput);
        // Limpia el campo de entrada después de enviar el mensaje
        setMessageInput('');
    };

    return (
        <div>
            {/* Renderizamos los mensajes */}
            <div>
                {messages.map((message, index) => (
                    <div key={index}>{message}</div>
                ))}
            </div>

            {/* Formulario para enviar mensajes */}
            <form onSubmit={sendMessage}>
                <input
                    type="text"
                    value={messageInput}
                    onChange={(e) => setMessageInput(e.target.value)}
                    placeholder="Escribe tu mensaje aquí..."
                />
                <button type="submit">Enviar</button>
            </form>
        </div>
    );
};

export default Chat;




























// form.js

import  { useState } from 'react';

const Form = () => {
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');

    const handleSubmit = (e) => {
        e.preventDefault();
        // Aquí puedes manejar la lógica para el inicio de sesión
        console.log("Inicio de sesión con:", email, password);
    };

    return (
        <div>
            <h2>Iniciar sesión</h2>
            <form onSubmit={handleSubmit}>
                <input type="email" placeholder="Email" value={email} onChange={(e) => setEmail(e.target.value)} />
                <input type="password" placeholder="Contraseña" value={password} onChange={(e) => setPassword(e.target.value)} />
                <button type="submit">Iniciar sesión</button>
            </form>
        </div>
    );
};

export default Form;























import  { useState } from 'react';

const Login = () => {
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');

    const handleSubmit = (e) => {
        e.preventDefault();
        // Aquí podrías manejar la lógica para iniciar sesión
    };

    return (
        <div>
            <h2>Iniciar sesión</h2>
            <form onSubmit={handleSubmit}>
                <input type="email" placeholder="Email" value={email} onChange={(e) => setEmail(e.target.value)} />
                <input type="password" placeholder="Contraseña" value={password} onChange={(e) => setPassword(e.target.value)} />
                <button type="submit">Iniciar sesión</button>
            </form>
        </div>
    );
};

export default Login;





