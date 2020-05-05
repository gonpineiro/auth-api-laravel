# auth-api-laravel
Modelo de auth para utilizar API en Laravel

### 1) Agregar la etiqueta META en el app.blade.php para traer el Token

```
    @if (auth()->check())
        <meta name="api-token" content="{{ auth()->user()->api_token }}">
    @endif 
```

### 2) Agregar el siguente código en bootstrap.js

```
    let token = document.head.querySelector('meta[name="csrf-token"]');

    if (token) {
        window.axios.defaults.headers.common['X-CSRF-TOKEN'] = token.content;
    } else {
        console.error('CSRF token not found: https://laravel.com/docs/csrf#csrf-x-csrf-token');
    }

    let api_token = document.head.querySelector('meta[name="api-token"]');

    if (api_token) {
    window.axios.defaults.headers.common['Authorization'] = 'Bearer ' + api_token.content;
    }
```

### 3) En la tabla de Ususuarios, debera contener una columna donde se cree un token aleatoriamente.

##### Cambiamos la migration de users para que el "create" genere dicho registro.

```
    protected function create(array $data)
        {
            return User::create([
                'name' => $data['name'],
                'email' => $data['email'],
                'password' => bcrypt($data['password']),
                'api_token' => Str::random(60),
            ]);
        }
    
```
##### Requiere la siguente Dependencia:

```
    use Illuminate\Support\Str;
```