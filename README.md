Awilix
Awilix es una librería para manejar la inyección de dependencias en Node.js. Es útil para organizar y gestionar las dependencias de tu aplicación de manera modular.
Instalar Awilix:
npm install awilix
Ejemplo de código:

// index.js
const { createContainer, asClass, asValue, asFunction } = require('awilix');

// Servicios (dependencias)
class UserService {
    constructor({ userRepository }) {
        this.userRepository = userRepository;
    }

    getUsers() {
        return this.userRepository.getUsers();
    }
}

class UserRepository {
    getUsers() {
        return ['User1', 'User2', 'User3'];
    }
}

// Contenedor de Awilix
const container = createContainer();

// Registrar dependencias
container.register({
    userService: asClass(UserService).singleton(),
    userRepository: asClass(UserRepository).singleton(),
});

// Resolver y usar el servicio
const userService = container.resolve('userService');
console.log(userService.getUsers()); // ['User1', 'User2', 'User3']
