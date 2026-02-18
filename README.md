# PHP Notes Application (Custom Mini Framework)

A simple Notes application built on top of a custom PHP micro-framework created from scratch.

This project includes:

- Custom Router
- Dependency Injection Container
- Middleware system (auth / guest)
- Authentication system
- Session & Flash handling
- Validation & Exception flow
- Notes CRUD
- Composer autoload (PSR-4)
- Pest testing setup

This project demonstrates backend fundamentals without using Laravel or other full frameworks.

---

#Features

#Authentication
- Register
- Login
- Logout
- Guest middleware
- Auth middleware
- Password hashing (bcrypt)

#Notes CRUD
- Create note
- View all notes
- View single note
- Edit note
- Update note
- Delete note
- Authorization check per note

#Core Architecture
- Custom Router
- Middleware resolver
- Dependency Injection Container
- App container static access
- Custom Database wrapper (PDO)
- ValidationException with redirect back
- Session flash data
- Global helper functions

---

#Project Structure

php_notes_application/
│
├── Core/
│ ├── App.php
│ ├── Authenticator.php
│ ├── Container.php
│ ├── Database.php
│ ├── Response.php
│ ├── Router.php
│ ├── Session.php
│ ├── ValidationException.php
│ ├── Validator.php
│ ├── functions.php
│ └── Middleware/
│ ├── Middleware.php
│ ├── Guest.php
│ └── Authenticated.php
│
├── Http/
│ ├── controllers/
│ │ ├── notes/
│ │ ├── registration/
│ │ └── session/
│ └── Forms/
│ └── LoginForm.php
│
├── public/
│ ├── index.php
│ └── playground.php
│
├── views/
│ ├── notes/
│ ├── registration/
│ ├── session/
│ ├── partials/
│ ├── 403.php
│ ├── 404.php
│ └── index.view.php
│
├── tests/
│ ├── Feature/
│ ├── Unit/
│ └── Pest.php
│
├── bootstrap.php
├── config.php
├── routes.php
├── composer.json
└── phpunit.xml


---

#Installation

#Clone the repository

bash
git clone https://github.com/your-username/php_notes_application.git
cd php_notes_application
 Install dependencies
composer install
Setup Database
Create a MySQL database:

myapp
Update config.php if needed:

return [
    'database' => [
        'host' => 'localhost',
        'port' => 3306,
        'dbname' => 'myapp',
        'charset' => 'utf8mb4'
    ]
];
Create tables
Example schema:

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL
);

CREATE TABLE notes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    body TEXT NOT NULL,
    user_id INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
Run the application
Point your server root to the public/ folder.

Or run with PHP built-in server:

php -S localhost:8000 -t public
Then open:

http://localhost:8000
Architecture Overview
Router
Handles:

GET

POST

PATCH

DELETE

Middleware per route

Routes are defined in:

routes.php
Dependency Injection Container
The app uses a custom container:

App::resolve(Database::class);
Bindings are defined in:

bootstrap.php
Middleware System
Middleware is mapped via:

Middleware::MAP = [
    'guest' => Guest::class,
    'auth' => Authenticated::class
];
Routes can use:

$router->get('/notes', 'notes/index.php')->only('auth');
Validation Flow
Validation can throw:

ValidationException::throw($errors, $old);
Which is caught in:

public/index.php
And redirects back with flash session data.

Session & Flash
Custom flash system:

Session::flash('errors', $errors);
Session::unflash();
Testing
This project includes Pest configuration.

Run tests:

vendor/bin/pest
What This Project Demonstrates
Understanding of HTTP routing

Middleware patterns

Authentication flow

Dependency Injection

Custom framework architecture

Exception-driven validation

Secure password handling

PDO usage

Clean project structure

Tech Stack
PHP

MySQL

Composer

Pest

PHPUnit

TailwindCSS (CDN)

Future Improvements
Proper user-based note filtering (currently hardcoded user_id)

CSRF protection

API version

JSON responses

Better folder separation (Controllers vs Handlers)

Proper migration system
