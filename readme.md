# [Material Dashboard Laravel - Free Frontend Preset for Laravel](https://material-dashboard-laravel.creative-tim.com/?ref=adnp-readme)


![Product Image](https://s3.amazonaws.com/creativetim_bucket/products/154/original/opt_md_laravel_thumbnail.jpg?1554814177)

Speed up your web development with the Bootstrap 4 Admin Dashboard built for Laravel Framework 5.5 and up.

## Note

We recommend installing this preset on a project that you are starting from scratch, otherwise your project's design might break.

## Prerequisites

If you don't already have an Apache local environment with PHP and MySQL, use one of the following links:

 - Windows: https://updivision.com/blog/post/beginner-s-guide-to-setting-up-your-local-development-environment-on-windows
 - Linux: https://howtoubuntu.org/how-to-install-lamp-on-ubuntu
 - Mac: https://wpshout.com/quick-guides/how-to-install-mamp-on-your-mac/

Also, you will need to install Composer: https://getcomposer.org/doc/00-intro.md   
And Laravel: https://laravel.com/docs/7.x/installation

## Installation

After initializing a fresh instance of Laravel (and making all the necessary configurations), install the preset using one of the provided methods:

### Via composer

1. `Cd` to your Laravel app  
2. Type in your terminal: `composer require laravel/ui` and `php artisan ui vue --auth`
3. Install this preset via `composer require laravel-frontend-presets/material-dashboard`. No need to register the service provider. Laravel 5.5 & up can auto detect the package.
4. Run `php artisan ui material` command to install the Argon preset. This will install all the necessary assets and also the custom auth views, it will also add the auth route in `routes/web.php`
(NOTE: If you run this command several times, be sure to clean up the duplicate Auth entries in routes/web.php)
5. In your terminal run `composer dump-autoload`
6. Run `php artisan migrate --seed` to create basic users table

### By using the archive

1. In your application's root create a **presets** folder
2. [Download an archive](https://github.com/laravel-frontend-presets/material-dashboard/archive/master.zip) of the repo and unzip it
3. Copy and paste **material-dashboard-master** folder in presets (created in step 2) and rename it to **material**
4. Open `composer.json` file 
5. Add `"LaravelFrontendPresets\\MaterialPreset\\": "presets/material/src"` to `autoload/psr-4` and to `autoload-dev/psr-4`
6. Add `LaravelFrontendPresets\MaterialPreset\MaterialPresetServiceProvider::class` to `config/app.php` file
7. Type in your terminal: `composer require laravel/ui` and `php artisan ui vue --auth`
8. In your terminal run `composer dump-autoload`
9. Run `php artisan ui material` command to install the Material preset. This will install all the necessary assets and also the custom auth views, it will also add the auth route in `routes/web.php`
(NOTE: If you run this command several times, be sure to clean up the duplicate Auth entries in routes/web.php)
10. Run `php artisan migrate --seed` to create basic users table


## Usage

Register a user or login using **admin@material.com** and **secret** and start testing the preset (make sure to run the migrations and seeders for these credentials to be available).

Besides the dashboard and the auth pages this preset also has an edit profile page. All the necessary files (controllers, requests, views) are installed out of the box and all the needed routes are added to `routes/web.php`. Keep in mind that all of the features can be viewed once you login using the credentials provided above or by registering your own user. 

### Dashboard

You can access the dashboard either by using the "**Dashboard**" link in the left sidebar or by adding **/home** in the url. 

### Profile edit

You have the option to edit the current logged in user's profile (change name, email and password). To access this page just click the "**User profile**" link in the left sidebar or by adding **/profile** in the url.

The `App\Http\Controllers\ProfileController` handles the update of the user information. 

```
public function update(ProfileRequest $request)
{
    auth()->user()->update($request->all());

    return back()->withStatus(__('Profile successfully updated.'));
}
```

Also you shouldn't worry about entering wrong data in the inputs when editing the profile, validation rules were added to prevent this (see `App\Http\Requests\ProfileRequest`). If you try to change the password you will see that other validation rules were added in `App\Http\Requests\PasswordRequest`. Notice that in this file you have a custom validation rule that can be found in `App\Rules\CurrentPasswordCheckRule`.

```
public function rules()
{
    return [
        'old_password' => ['required', 'min:6', new CurrentPasswordCheckRule],
        'password' => ['required', 'min:6', 'confirmed', 'different:old_password'],
        'password_confirmation' => ['required', 'min:6'],
    ];
}
```
## Table of Contents

* [Versions](#versions)
* [Demo](#demo)
* [Documentation](#documentation)
* [File Structure](#file-structure)
* [Browser Support](#browser-support)
* [Resources](#resources)
* [Reporting Issues](#reporting-issues)
* [Licensing](#licensing)
* [Useful Links](#useful-links)

## Demo

| Register | Login | Dashboard |
| --- | --- | ---  |
| [![Register](/screens/Register.png)](https://material-dashboard-laravel.creative-tim.com/register?ref=mdl-readme)  | [![Login](/screens/Login.png)](https://material-dashboard-laravel.creative-tim.com/login?ref=mdl-readme)  | [![Dashboard](/screens/Dashboard.png)](https://material-dashboard-laravel.creative-tim.com/?ref=mdl-readme)

| Profile Page | Users Page | Tables Page  |
| --- | --- | ---  |
| [![Profile Page](screens/Profile.png)](https://material-dashboard-laravel.creative-tim.com/profile?ref=mdlp-readme)  | [![Users Page](screens/Users.png)](https://material-dashboard-laravel.creative-tim.com/user?ref=mdl-readme) | [![Tables Page](screens/Tables.png)](https://material-dashboard-laravel.creative-tim.com/table-list?ref=mdl-readme)


## File Structure
```
+---app
|   +---Http
|   |   +---Controllers
|   |   |       HomeController.php
|   |   |       ProfileController.php
|   |   |       UserController.php
|   |   |       
|   |   \---Requests
|   |           PasswordRequest.php
|   |           ProfileRequest.php
|   |           UserRequest.php
|   |           
|   \---Rules
|           CurrentPasswordCheckRule.php
|           
+---database
|   \---seeds
|           DatabaseSeeder.php
|           UsersTableSeeder.php
|           
\---resources
    +---assets
    |   +---css
    |   |       material-dashboard-rtl.css
    |   |       material-dashboard.css
    |   |       material-dashboard.css.map
    |   |       material-dashboard.min.css
    |   |       
    |   +---demo
    |   |       demo.css
    |   |       demo.js
    |   |       
    |   +---img
    |   +---js
    |   |   |   material-dashboard.js
    |   |   |   material-dashboard.js.map
    |   |   |   material-dashboard.min.js
    |   |   |   settings.js
    |   |   |   
    |   |   +---core
    |   |   |       bootstrap-material-design.min.js
    |   |   |       jquery.min.js
    |   |   |       popper.min.js
    |   |   |       
    |   |   \---plugins
    |   |           arrive.min.js
    |   |           bootstrap-datetimepicker.min.js
    |   |           bootstrap-notify.js
    |   |           bootstrap-selectpicker.js
    |   |           bootstrap-tagsinput.js
    |   |           chartist.min.js
    |   |           fullcalendar.min.js
    |   |           jasny-bootstrap.min.js
    |   |           jquery-jvectormap.js
    |   |           jquery.bootstrap-wizard.js
    |   |           jquery.dataTables.min.js
    |   |           jquery.tagsinput.js
    |   |           jquery.validate.min.js
    |   |           moment.min.js
    |   |           nouislider.min.js
    |   |           perfect-scrollbar.jquery.min.js
    |   |           sweetalert2.js
    |   |           
    |   \---scss
    |       |   material-dashboard.scss
    |       |   
    |       \---material-dashboard
    |           |   _alerts.scss
    |           |   _buttons.scss
    |           |   _cards.scss
    |           |   _checkboxes.scss
    |           |   _core-bootstrap.scss
    |           |   _dropdown.scss
    |           |   _example-pages.scss
    |           |   _fixed-plugin.scss
    |           |   _footers.scss
    |           |   _forms.scss
    |           |   _headers.scss
    |           |   _images.scss
    |           |   _info-areas.scss
    |           |   _input-group.scss
    |           |   _misc.scss
    |           |   _mixins.scss
    |           |   _navbar.scss
    |           |   _popover.scss
    |           |   _popups.scss
    |           |   _radios.scss
    |           |   _responsive.scss
    |           |   _ripples.scss
    |           |   _sidebar-and-main-panel.scss
    |           |   _social-buttons.scss
    |           |   _tables.scss
    |           |   _tabs.scss
    |           |   _togglebutton.scss
    |           |   _tooltip.scss
    |           |   _type.scss
    |           |   _variables.scss
    |           |   
    |           +---bootstrap
    |           |   \---scss
    |           |       |   bootstrap-grid.scss
    |           |       |   bootstrap-reboot.scss
    |           |       |   bootstrap.scss
    |           |       |   _alert.scss
    |           |       |   _badge.scss
    |           |       |   _breadcrumb.scss
    |           |       |   _button-group.scss
    |           |       |   _buttons.scss
    |           |       |   _card.scss
    |           |       |   _carousel.scss
    |           |       |   _close.scss
    |           |       |   _code.scss
    |           |       |   _custom-forms.scss
    |           |       |   _dropdown.scss
    |           |       |   _forms.scss
    |           |       |   _functions.scss
    |           |       |   _grid.scss
    |           |       |   _images.scss
    |           |       |   _input-group.scss
    |           |       |   _jumbotron.scss
    |           |       |   _list-group.scss
    |           |       |   _media.scss
    |           |       |   _mixins.scss
    |           |       |   _modal.scss
    |           |       |   _nav.scss
    |           |       |   _navbar.scss
    |           |       |   _pagination.scss
    |           |       |   _popover.scss
    |           |       |   _print.scss
    |           |       |   _progress.scss
    |           |       |   _reboot.scss
    |           |       |   _root.scss
    |           |       |   _tables.scss
    |           |       |   _tooltip.scss
    |           |       |   _transitions.scss
    |           |       |   _type.scss
    |           |       |   _utilities.scss
    |           |       |   _variables.scss
    |           |       |   
    |           |       +---mixins
    |           |       |       _alert.scss
    |           |       |       _background-variant.scss
    |           |       |       _badge.scss
    |           |       |       _border-radius.scss
    |           |       |       _box-shadow.scss
    |           |       |       _breakpoints.scss
    |           |       |       _buttons.scss
    |           |       |       _caret.scss
    |           |       |       _clearfix.scss
    |           |       |       _float.scss
    |           |       |       _forms.scss
    |           |       |       _gradients.scss
    |           |       |       _grid-framework.scss
    |           |       |       _grid.scss
    |           |       |       _hover.scss
    |           |       |       _image.scss
    |           |       |       _list-group.scss
    |           |       |       _lists.scss
    |           |       |       _nav-divider.scss
    |           |       |       _navbar-align.scss
    |           |       |       _pagination.scss
    |           |       |       _reset-text.scss
    |           |       |       _resize.scss
    |           |       |       _screen-reader.scss
    |           |       |       _size.scss
    |           |       |       _table-row.scss
    |           |       |       _text-emphasis.scss
    |           |       |       _text-hide.scss
    |           |       |       _text-truncate.scss
    |           |       |       _transition.scss
    |           |       |       _visibility.scss
    |           |       |       
    |           |       \---utilities
    |           |               _align.scss
    |           |               _background.scss
    |           |               _borders.scss
    |           |               _clearfix.scss
    |           |               _display.scss
    |           |               _embed.scss
    |           |               _flex.scss
    |           |               _float.scss
    |           |               _position.scss
    |           |               _screenreaders.scss
    |           |               _sizing.scss
    |           |               _spacing.scss
    |           |               _text.scss
    |           |               _visibility.scss
    |           |               
    |           +---cards
    |           |       _card-plain.scss
    |           |       _card-profile.scss
    |           |       _card-stats.scss
    |           |       
    |           +---mixins
    |           |       _alert.scss
    |           |       _animations.scss
    |           |       _breakpoints.scss
    |           |       _buttons.scss
    |           |       _chartist.scss
    |           |       _colored-shadows.scss
    |           |       _drawer.scss
    |           |       _forms.scss
    |           |       _hover.scss
    |           |       _layout.scss
    |           |       _navbar-colors.scss
    |           |       _navs.scss
    |           |       _sidebar-color.scss
    |           |       _transparency.scss
    |           |       _type.scss
    |           |       _utilities.scss
    |           |       _variables.scss
    |           |       _vendor-prefixes.scss
    |           |       
    |           +---plugins
    |           |       _animate.scss
    |           |       _chartist.scss
    |           |       _perfect-scrollbar.scss
    |           |       
    |           \---variables
    |                   _body.scss
    |                   _bootstrap-material-design-base.scss
    |                   _bootstrap-material-design.scss
    |                   _brand.scss
    |                   _buttons.scss
    |                   _card.scss
    |                   _code.scss
    |                   _colors-map.scss
    |                   _colors.scss
    |                   _custom-forms.scss
    |                   _drawer.scss
    |                   _dropdown.scss
    |                   _forms.scss
    |                   _layout.scss
    |                   _list-group.scss
    |                   _menu.scss
    |                   _modals.scss
    |                   _nav.scss
    |                   _pagination.scss
    |                   _shadow.scss
    |                   _snackbar.scss
    |                   _spacing.scss
    |                   _state.scss
    |                   _tables.scss
    |                   _tooltip.scss
    |                   _type.scss
    |                   
    \---views
        |   dashboard.blade.php
        |   home.blade.php
        |   welcome.blade.php
        |   
        +---auth
        |   |   login.blade.php
        |   |   register.blade.php
        |   |   verify.blade.php
        |   |   
        |   \---passwords
        |           email.blade.php
        |           reset.blade.php
        |           
        +---layouts
        |   |   app.blade.php
        |   |   
        |   +---footers
        |   |       auth.blade.php
        |   |       guest.blade.php
        |   |       
        |   +---navbars
        |   |   |   sidebar.blade.php
        |   |   |   
        |   |   \---navs
        |   |           auth.blade.php
        |   |           guest.blade.php
        |   |           
        |   \---page_templates
        |           auth.blade.php
        |           guest.blade.php
        |           
        +---pages
        |       icons.blade.php
        |       language.blade.php
        |       map.blade.php
        |       notifications.blade.php
        |       table_list.blade.php
        |       typography.blade.php
        |       upgrade.blade.php
        |       
        +---profile
        |       edit.blade.php
        |       
        \---users
                index.blade.php
```

## Browser Support

At present, we officially aim to support the last two versions of the following browsers:

<img src="https://github.com/creativetimofficial/public-assets/blob/master/logos/chrome-logo.png?raw=true" width="64" height="64"> <img src="https://raw.githubusercontent.com/creativetimofficial/public-assets/master/logos/firefox-logo.png" width="64" height="64"> <img src="https://raw.githubusercontent.com/creativetimofficial/public-assets/master/logos/edge-logo.png" width="64" height="64"> <img src="https://raw.githubusercontent.com/creativetimofficial/public-assets/master/logos/safari-logo.png" width="64" height="64"> <img src="https://raw.githubusercontent.com/creativetimofficial/public-assets/master/logos/opera-logo.png" width="64" height="64">


