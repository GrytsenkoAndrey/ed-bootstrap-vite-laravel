# ed-bootstrap-vite-laravel
How to use Bootstrap5 with Vite in Laravel9

### What is Bootstrap?

Bootstrap is a free and open-source web development framework. It’s designed to ease the web development process of responsive, mobile-first websites by providing a collection of syntax for template designs.

In other words, Bootstrap helps web developers build websites faster as they don’t need to worry about basic commands and functions. It consists of HTML, CSS, and JS-based scripts for various web design-related functions and components.

Bootstrap 5 is the newest version of Bootstrap.


## Features of Bootstrap


### 1. Easy to Begin With

It is pretty easy, to begin with. Being easy to get started with is probably the first quality that makes Bootstrap very appealing.

### 2. LESS as Well as CSS Files

Bootstrap not only offers LESS files but also includes the old CSS files.


### 3. Easily Customizable

Despite the fact that Bootstrap is designed in responsive 12-column grids, layouts, and components, it is also very easy to customize. Whether you need a fixed grid or a responsive one, it can be made possible by making a few changes. Offsetting and nesting columns are also easy to do in both CPU-based and mobile-based browser grids.


### 4. Responsive Utility Classes

Another prominent feature of Bootstrap is its responsive utility classes. Using responsive utility classes, a particular piece of content can be made to appear or hide only on devices depending on the size of the screen being used. This feature is extremely helpful for designers who want to make a mobile and tablet-friendly version of their websites.


### 5. Components of Bootstrap

Some of the components that come pre-styled in Bootstrap are:

- Drop-downs
- Button
- Navigation
- Badges
- Alerts
- Progress Bar

### 6. Drop-Down Component Menu

The drop-down component menu is a responsive additive feature of a website. To include it in a website, a lot of different plugins, mostly Java-based, are tested. But, via Bootstrap and its easy customizing options, this can easily be done in a matter of minutes.

### 7. Bootstrap Templates

The readily available templates make it easier for inexperienced users to create a website following a simple tutorial or demo available on Bootstrap.

### What is Vite?

Vite (the French word for "quick", pronounced /vit/ , like "veet") is a build tool that aims to provide a faster and leaner development experience for modern web projects.

### Features of Vite

- Instant Server Start
- Lightning Fast HMR (Hot Module Replacement)
- Support for TypeScript, JSX, CSS, and more.
- Optimized Build
- Universal Plugins
- Fully Typed APIs

Laravel has just released **“laravel 9.19”** with a major change. There is no more **webpack.mix.js** file in the laravel root in the place of the **webpack.mix.js** file **vite.config.js** file is introduced.

In this section we will install bootstrap 5 in laravel 9 with vite. In laravel 9.19 come with vite tool, we will install bootstrap 5 in laravel 9 with larave ui.

### How to Install Bootstrap 5 in Laravel 9 With Vite

Use the following steps to install Bootstrap 5 in the laravel 9 with Vite.

<ol>
    <li>Install Laravel Project</li>
    <li>Install Laravel UI For Bootstrap 5</li>
    <li>Setup Auth Scaffolding with Bootstrap 5</li>
    <li>Install NPM Dependencies</li>
    <li>Import vite.config.js Bootstrap 5 Path</li>
    <li>Update bootstrap.js</li>
    <li>Import Bootstrap 5 SCSS in JS Folder</li>
    <li>Replace mix() with @vite Blade directive</li>
    <li>Running Vite Command to build Asset File</li>
    <li>Start the Local server</li>
</ol>

----------------------------------------------------------------
### Step 1: Install Laravel Project

Installing a fresh new laravel application, so head over to the terminal, type the command, and create a new laravel app.

```composer create-project --prefer-dist laravel/laravel:^9.0 laravel9-bootstrap5-vite```

or, if you have installed the Laravel Installer as a global composer dependency:

```laravel new laravel9-bootstrap5-vite```

### Step 2: Install Laravel UI For Bootstrap 5

Next, you need to run the below command in your terminal

```composer require laravel/ui```

### Step 3: Setup Auth Scaffolding with Bootstrap 5

```php artisan ui bootstrap --auth```

 ### Step 4: Install NPM Dependencies

Run the following command to install frontend dependencies:

```npm install```

### Step 5: Import vite.config.js Bootstrap 5 Path

First, you need to change vite.config.js and add the bootstrap 5 path & remove resources/css/app.css

```
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import path from 'path'

export default defineConfig({
    plugins: [
        laravel([
            'resources/js/app.js',
        ]),
    ],
    resolve: {
        alias: {
            '~bootstrap': path.resolve(__dirname, 'node_modules/bootstrap'),
        }
    },
});
```

### Step 6: Update bootstrap.js

We need to use import instead of require.

```
import loadash from 'lodash'
window._ = loadash


import * as Popper from '@popperjs/core'
window.Popper = Popper

import 'bootstrap'


/**
 * We'll load the axios HTTP library which allows us to easily issue requests
 * to our Laravel back-end. This library automatically handles sending the
 * CSRF token as a header based on the value of the "XSRF" token cookie.
 */

import axios from 'axios'
window.axios = axios

window.axios.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest';

/**
 * Echo exposes an expressive API for subscribing to channels and listening
 * for events that are broadcast by Laravel. Echo and event broadcasting
 * allows your team to easily build robust real-time web applications.
 */

// import Echo from 'laravel-echo';

// window.Pusher = require('pusher-js');

// window.Echo = new Echo({
//     broadcaster: 'pusher',
//     key: process.env.MIX_PUSHER_APP_KEY,
//     cluster: process.env.MIX_PUSHER_APP_CLUSTER,
//     forceTLS: true
// });
```

### Step 7: Import Bootstrap 5 SCSS in JS Folder

Now you need to import bootstrap 5 SCSS path in you resources/js/app.js or resources/js/bootstrap.js

```
resources/js/app.js

import './bootstrap';

import '../sass/app.scss'
```

### Step 8: Replace mix() with @vite Blade directive

When using Vite, you will need to use the @vite Blade directive instead of the mix() helper. remove mix helper and add @vite directive.

```
<link rel="stylesheet" href="{{ mix('css/app.css') }}">
<script src="{{ mix('js/app.js') }}" defer></script>
```

use @vite directive

```
@vite(['resources/js/app.js'])
```

views/layouts/app.blade

```
<!doctype html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- CSRF Token -->
    <meta name="csrf-token" content="{{ csrf_token() }}">

    <title>{{ config('app.name', 'Laravel') }}</title>

    <!-- Fonts -->
    <link rel="dns-prefetch" href="//fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css?family=Nunito" rel="stylesheet">

    @vite(['resources/js/app.js'])

</head>
<body>
    <div id="app">
        <nav class="navbar navbar-expand-md navbar-light bg-white shadow-sm">
            <div class="container">
                <a class="navbar-brand" href="{{ url('/') }}">
                    {{ config('app.name', 'Laravel') }}
                </a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="{{ __('Toggle navigation') }}">
                    <span class="navbar-toggler-icon"></span>
                </button>

                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <!-- Left Side Of Navbar -->
                    <ul class="navbar-nav me-auto">

                    </ul>

                    <!-- Right Side Of Navbar -->
                    <ul class="navbar-nav ms-auto">
                        <!-- Authentication Links -->
                        @guest
                            @if (Route::has('login'))
                                <li class="nav-item">
                                    <a class="nav-link" href="{{ route('login') }}">{{ __('Login') }}</a>
                                </li>
                            @endif

                            @if (Route::has('register'))
                                <li class="nav-item">
                                    <a class="nav-link" href="{{ route('register') }}">{{ __('Register') }}</a>
                                </li>
                            @endif
                        @else
                            <li class="nav-item dropdown">
                                <a id="navbarDropdown" class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown" aria-haspopup="true" aria-expanded="false" v-pre>
                                    {{ Auth::user()->name }}
                                </a>

                                <div class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                                    <a class="dropdown-item" href="{{ route('logout') }}"
                                       onclick="event.preventDefault();
                                                     document.getElementById('logout-form').submit();">
                                        {{ __('Logout') }}
                                    </a>

                                    <form id="logout-form" action="{{ route('logout') }}" method="POST" class="d-none">
                                        @csrf
                                    </form>
                                </div>
                            </li>
                        @endguest
                    </ul>
                </div>
            </div>
        </nav>

        <main class="py-4">
            @yield('content')
        </main>
    </div>
</body>
</html>
```

### Step 9: Running Vite Command to build Asset File

You need to npm run build command to create asset bootstrap 5.

```npm run build```

### Step 10: Start the Local server

Now open a new terminal and execute the following command from your terminal to run the development server.

```php artisan serve```

and navigate to the following link **http://localhost:8000/**

[Article](https://techvblogs.com/blog/how-to-install-bootstrap-5-in-laravel-9-with-vite)
