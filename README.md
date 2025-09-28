# Chat Server Java

Un serveur de chat multi-client simple implémenté en Java utilisant les sockets TCP/IP et la programmation multi-threadée.

## 🎯 Concepts utilisés

### **Programmation réseau avec Sockets**
- **Socket TCP/IP** : Établit des connexions fiables entre le serveur et les clients
- **ServerSocket** : Écoute les connexions entrantes sur le port 12354
- **BufferedReader/PrintWriter** : Gestion des flux d'entrée/sortie pour la communication

### **Programmation multi-threadée**
- **Thread principal** : Le serveur accepte les nouvelles connexions en continu
- **Threads clients** : Chaque client est géré dans un thread séparé via `ClientHandler`
- **Thread de lecture** : Dans le client, un thread dédié écoute les messages du serveur

### **Gestion des collections concurrentes**
- **Collections.synchronizedSet()** : Assure la thread-safety pour la liste des clients connectés
- **Synchronisation** : Blocs synchronized pour éviter les conditions de course lors du broadcast

### **Pattern Producer-Consumer**
- Les clients produisent des messages
- Le serveur consomme et redistribue les messages à tous les autres clients

### **Gestion des ressources**
- **Try-with-resources** : Fermeture automatique des sockets et flux
- **Gestion des exceptions** : Traitement propre des erreurs de connexion

## 🏗️ Architecture

```
ChatServer
├── Écoute sur le port 12354
├── Maintient une liste des clients connectés
└── Gère le broadcast des messages

ClientHandler (un par client)
├── Thread dédié pour chaque connexion
├── Lit les messages du client
└── Notifie le serveur pour broadcast

ChatClient
├── Se connecte au serveur
├── Thread pour recevoir les messages
└── Thread principal pour envoyer les messages
```

## 🚀 Installation et exécution

### Prérequis
- Java JDK 8 ou supérieur
- 3 terminaux disponibles

### Compilation
```bash
javac *.java
```

### Exécution

#### Terminal 1 - Serveur
```bash
java ChatServer
```

#### Terminal 2 - Client 1
```bash
java ChatClient
```

#### Terminal 3 - Client 2
```bash
java ChatClient
```

## 📝 Utilisation

1. **Démarrer le serveur** : Lance le serveur qui attend les connexions
2. **Connecter les clients** : Les clients se connectent automatiquement au serveur
3. **Échanger des messages** : Tapez vos messages dans un terminal client, ils apparaîtront dans l'autre

### Exemple de session
```
Terminal Client 1: Hello from Client 1!
Terminal Client 2: Received: Hello from Client 1!

Terminal Client 2: Hi there!
Terminal Client 1: Received: Hi there!
```

## 🔧 Fonctionnalités

- **Communication bidirectionnelle** entre tous les clients connectés
- **Gestion automatique des déconnexions** des clients
- **Support multi-clients** simultanés
- **Messages en temps réel** via broadcasting

## 📚 Points d'apprentissage

Ce projet illustre parfaitement :
- La programmation réseau en Java
- La gestion de la concurrence et des threads
- Les patterns de communication client-serveur
- La synchronisation des ressources partagées
- La gestion propre des ressources système
