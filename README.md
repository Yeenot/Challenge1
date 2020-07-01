# Guidelines

- [1. Visual Studio Code Packages](#1-visual-studio-code-packages)
- [2. File structure](#2-coding-specifications)
  - [2.1. Controllers](#21-controllers)
  - [2.2. Javascript](#22-javascript)
  - [2.3. Assets](#23-assets)
  - [2.4. Lang](#24-lang)
  - [2.5. Views](#25-views)
- [3. Action classes pattern](#3-action-classes-pattern)
- [4. Form requests](#4-form-requests)
- [5. Models](#5-form-requests)
  - [5.1. Scopes](#51-controllers)
  - [5.2. Relationships](#52-javascript)
- [6. Routes](#6-routes)
  - [6.1. File structure](#61-assets)
  - [6.2. Naming](#62-naming)
- [7. Don't repeat yourself (DRY)](#7-dont-repeat-yourself)
- [8. General rules](#8-general-rules)

# 1. Visual Studio Code Packages
Install the following packages
 - php-cs-fixer
 - PHP Intelephense
 - ESLint
 - Prettier
 - GitLens
 - PHP DocBlocker

# 2. File structure

## 2.1 Controllers
- **Staff**- `app\Http\Controllers\Staff\{ModuleName}`
- **Public**- `app\Http\Controllers\Public`
- **Ajax**- `app\Http\Controllers\Ajax`
- **API**- `app\Http\Controllers\API`

## 2.2 Javascript
- **Staff** - `resources/js/staff/{module-name}`
- **Public** - `resources/js/public`
   - `resources/js/staff/countries`

## 2.3 Assets
- **Staff** - `resources/assets/staff/{module-name}`
- **Public** - `resources/assets/public`

## 2.4 Lang
- **Staff** - `resources/lang/en/staff`
- **Public** - `resources/lang/en/public`

## 2.5 Views
- **Staff** - `templates/staff/{module-name}`
- **Public** - `templates/public`

# 3. Action classes pattern
Use action classes for bussiness logic codes rather than controllers.  
path: `app\Services\{ModuleName}`

Example:
```
class GetUserByEmail 
{
    /**
     * Get user by email
     *
     * @param string $email
     * @return App\Models\User
     */
    public function execute(string $email)
    {
        return User::where('email', $email)->first();
    }
}
```

# 4. Form requests
Use form request instead of validating per controller methods.
path: `app\Http\Requests\{ModuleName}`
- 1 form request per item (create/update)
- Messages should be translated

Example:
```
class GetUserByEmail 
{
    /**
     * Get user by email
     *
     * @param string $email
     * @return App\Models\User
     */
    public function execute(string $email)
    {
        return User::where('email', $email)->first();
    }
}
```

# 5. Models

## 5.1 Scopes
Use scopes for reusability
```
public function scopeActive($q)
{
    return $q->where('is_active', 1);
}
```

## 5.2 Relationships
- names should be descriptive
- proper grammer
  - `one-to-one` - singular
  - `one-to-many` - plural

# 6. Routes

## 6.1 File structure
Proper segregation of route files
- `routes/staff.php`
- `routes/staff_ajax.php`
- `routes/public.php`
- `routes/public_ajax.php`
- `routes/api.php`

## 6.2 Naming
Example:
```Route::get('/group-companies', 'GroupCompanyController@index')->name('staff.group_companies.index')```
- public-facing urls must use kebab-case
- use `.` as a group separator
- use `_` as a name separator

# 7. Don't repeat yourself (DRY)
A class and a method should have only one responsibility so that it is readable and helps us to avoid code duplication.

```
public function getArticles()
{
    return $this->whereHas('user', function ($q) {
            $q->active();
        })->get();
}
```

# 8. General rules
- Proper indentions (per ***4 spaces***)
- Proper whitespace between codes
- Proper singular/plural naming
- Remove unused codes
- Comment your codes using ***Docblock***
- File/class names should be ***DESCRIPTIVE***
- Method names should be ***DESCRIPTIVE***
- All static texts/labels ***MUST*** be always translated
- ***DO NOT*** put logical codes in controllers, blades, and helpers

