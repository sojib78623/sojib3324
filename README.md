<?php

/**
 * Laravel-based Website Implementation
 * 
 * This script defines the main routes for the Laravel application, including authentication 
 * and CRUD operations for a sample entity (e.g., blog posts). 
 * 
 * Features:
 * - User Registration, Login, and Logout
 * - CRUD operations for posts (Create, Read, Update, Delete)
 * - Middleware for authentication protection
 * 
 * Technologies Used:
 * - Laravel Framework (PHP-based MVC)
 * - Blade Templating for frontend
 * - MySQL Database with Eloquent ORM
 * 
 * Author: [Your Name]
 * Date: [Insert Date]
 */

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\AuthController;
use App\Http\Controllers\PostController;

/**
 * Home Route
 * Displays the welcome page of the website.
 */
Route::get('/', function () {
    return view('welcome');
});

/**
 * Authentication Routes
 * Handles user registration, login, and logout.
 */
Route::get('/register', [AuthController::class, 'showRegisterForm']);
Route::post('/register', [AuthController::class, 'register']);
Route::get('/login', [AuthController::class, 'showLoginForm']);
Route::post('/login', [AuthController::class, 'login']);
Route::post('/logout', [AuthController::class, 'logout'])->middleware('auth');

/**
 * Protected Routes for CRUD Operations
 * Only accessible to authenticated users.
 */
Route::middleware(['auth'])->group(function () {
    Route::get('/posts', [PostController::class, 'index']); // List all posts
    Route::get('/posts/create', [PostController::class, 'create']); // Show form to create post
    Route::post('/posts', [PostController::class, 'store']); // Store new post
    Route::get('/posts/{id}', [PostController::class, 'show']); // View specific post
    Route::get('/posts/{id}/edit', [PostController::class, 'edit']); // Show edit form
    Route::put('/posts/{id}', [PostController::class, 'update']); // Update existing post
    Route::delete('/posts/{id}', [PostController::class, 'destroy']); // Delete post
});

?>
