PHP Notes Application

Custom-built PHP notes application powered by a lightweight framework written from scratch.

This project demonstrates understanding of backend architecture concepts without relying on Laravel or other full-stack frameworks.

Overview

The application includes:

Custom Router

Dependency Injection Container

Middleware system (auth / guest)

Authentication (register, login, logout)

Notes CRUD

Validation & Exception handling flow

Session & Flash messaging

PSR-4 Composer autoload

Basic Pest test setup

The goal of this project was to understand how modern frameworks work internally by implementing core features manually.

Key Features
Authentication

Secure password hashing (bcrypt)

Session-based login

Guest & Auth middleware protection

Notes Management

Create, edit, update and delete notes

Authorization check per note

Clean separation between controllers and views

Architecture
Routing

Custom Router supporting:

GET

POST

PATCH

DELETE

Per-route middleware

Routes are defined in routes.php.

Dependency Injection

A simple service container handles dependency resolution:

App::resolve(Database::class);


Bindings are configured in bootstrap.php.

Middleware

Middleware resolution is handled dynamically:

$router->get('/notes', 'notes/index.php')->only('auth');


Supported middleware:

auth

guest

Validation & Error Handling

Validation failures throw a custom ValidationException which is caught in the front controller and redirects back with flash session data.

Tech Stack

PHP (OOP)

MySQL (PDO)

Composer (PSR-4)

Pest (testing setup)

TailwindCSS (CDN)

Running Locally

Install dependencies:

composer install


Run with built-in PHP server:

php -S localhost:8000 -t public

Purpose of the Project

This project was built to deepen understanding of:

Routing mechanisms

Middleware pipelines

Dependency injection

Session management

Authentication flow

Clean backend structure

Author

Stefan Cirkovic
