## Capitulo 2.5 Modelos y el ORM Eloquent en Laravel

- ¿Cómo se trabaja con modelos y Eloquent ORM en Laravel?

 Ahora te explicaré cómo trabajar con modelos y Eloquent ORM en Laravel.

1. Crear un modelo:
En Laravel, los modelos se utilizan para interactuar con la base de datos. Puedes crear un modelo usando el comando Artisan `make:model`. Por ejemplo, si deseas crear un modelo llamado `User`, ejecuta el siguiente comando:

```shell
php artisan make:model User
```

Esto generará un archivo `User.php` en el directorio `app/Models` de tu proyecto Laravel. Puedes definir las propiedades y métodos del modelo dentro de este archivo.

2. Configurar la tabla asociada:
Por defecto, Eloquent asume que el nombre de la tabla asociada al modelo es el plural del nombre del modelo en minúsculas. Por ejemplo, para el modelo `User`, Eloquent buscará la tabla `users` en la base de datos. Si tu tabla tiene un nombre diferente, puedes especificarlo en el modelo utilizando la propiedad `$table`. Por ejemplo:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    protected $table = 'mi_tabla';
}
```

3. Definir relaciones:
Eloquent ORM permite definir relaciones entre modelos. Por ejemplo, si tienes un modelo `User` y un modelo `Post`, puedes definir una relación de uno a muchos entre ellos. Añade el siguiente método al modelo `User`:

```php
public function posts()
{
    return $this->hasMany(Post::class);
}
```

Esto establece la relación de uno a muchos entre un usuario y sus publicaciones.

4. Realizar consultas:
Eloquent proporciona una forma intuitiva de realizar consultas a la base de datos. Puedes encadenar métodos en el modelo para especificar las condiciones de la consulta. Aquí tienes algunos ejemplos:

- Obtener todos los usuarios:
```php
$users = User::all();
```

- Obtener un usuario por su ID:
```php
$user = User::find($id);
```

- Obtener usuarios que cumplan cierta condición:
```php
$users = User::where('age', '>', 18)->get();
```

Estos son solo ejemplos básicos, pero Eloquent ofrece muchas más opciones para realizar consultas avanzadas.

5. Realizar operaciones CRUD:
Eloquent facilita las operaciones CRUD (Crear, Leer, Actualizar y Eliminar). Aquí tienes algunos ejemplos:

- Crear un nuevo usuario:
```php
$user = new User;
$user->name = 'John Doe';
$user->email = 'john@example.com';
$user->save();
```

- Actualizar un usuario existente:
```php
$user = User::find($id);
$user->name = 'Jane Doe';
$user->save();
```

- Eliminar un usuario:
```php
$user = User::find($id);
$user->delete();
```

Estos son solo ejemplos básicos, pero Eloquent proporciona métodos más avanzados para realizar operaciones CRUD.

Recuerda importar el modelo al principio de tus archivos donde quieras utilizarlo:

```php
use App\Models\User;
```

Esto te permitirá acceder al modelo `User` en ese archivo.

Espero que esta guía te ayude a trabajar con modelos y Eloquent ORM en Laravel. Si tienes alguna pregunta adicional, no dudes en preguntar.

¡Claro! Continuemos con la guía sobre cómo trabajar con modelos y Eloquent ORM en Laravel.

6. Utilizar relaciones definidas:
Una vez que has definido relaciones entre modelos, puedes utilizarlas para acceder a los datos relacionados. Por ejemplo, si tienes un modelo `User` con una relación de uno a muchos hacia el modelo `Post`, puedes acceder a las publicaciones de un usuario de la siguiente manera:

```php
$user = User::find($userId);
$posts = $user->posts;
```

Esto te devolverá una colección de todas las publicaciones asociadas al usuario.

7. Definir relaciones inversas:
Además de las relaciones directas, también puedes definir relaciones inversas en tus modelos. Esto te permite acceder al modelo padre desde el modelo hijo. Por ejemplo, si tienes una relación de uno a muchos entre `User` y `Post`, puedes acceder al usuario asociado a una publicación de la siguiente manera:

En el modelo `Post`:
```php
public function user()
{
    return $this->belongsTo(User::class);
}
```

Luego, puedes acceder al usuario asociado a una publicación de esta manera:

```php
$post = Post::find($postId);
$user = $post->user;
```

Esto te devolverá el modelo `User` asociado a la publicación.

8. Utilizar consultas relacionales:
Eloquent ORM te permite realizar consultas que involucran relaciones entre modelos. Puedes encadenar métodos para especificar condiciones en las relaciones. Por ejemplo, si deseas obtener todos los usuarios con al menos una publicación, puedes hacerlo de la siguiente manera:

```php
$users = User::has('posts')->get();
```

Esto te devolverá una colección de usuarios que tienen al menos una publicación asociada.

Estos son solo algunos ejemplos de cómo trabajar con modelos y Eloquent ORM en Laravel. Eloquent proporciona una amplia gama de métodos y funcionalidades para interactuar con la base de datos de manera elegante y eficiente.

9. Utilizar consultas avanzadas:
Eloquent ORM proporciona una serie de métodos para realizar consultas avanzadas a la base de datos. Algunos ejemplos son:

- `whereHas`: Permite filtrar los modelos basándose en la existencia de una relación. Por ejemplo, si deseas obtener todos los usuarios que tengan al menos una publicación con una determinada etiqueta, puedes hacerlo de la siguiente manera:

  ```php
  $users = User::whereHas('posts', function ($query) use ($tag) {
      $query->whereHas('tags', function ($query) use ($tag) {
          $query->where('name', $tag);
      });
  })->get();
  ```

- `withCount`: Permite obtener el recuento de registros relacionados. Por ejemplo, si deseas obtener todos los usuarios junto con el número de publicaciones que tienen, puedes hacerlo de la siguiente manera:

  ```php
  $users = User::withCount('posts')->get();
  foreach ($users as $user) {
      echo "El usuario {$user->name} tiene {$user->posts_count} publicaciones.";
  }
  ```

10. Utilizar mutadores y accesores:
Eloquent ORM te permite definir mutadores y accesores en tus modelos para realizar transformaciones en los datos antes de guardarlos en la base de datos o antes de mostrarlos. Los mutadores permiten modificar el valor de un atributo antes de guardarlo, mientras que los accesores permiten modificar el valor de un atributo antes de mostrarlo. Por ejemplo:

  ```php
  class User extends Model
  {
      // Mutador
      public function setPasswordAttribute($value)
      {
          $this->attributes['password'] = bcrypt($value);
      }

      // Accesor
      public function getFullNameAttribute()
      {
          return "{$this->first_name} {$this->last_name}";
      }
  }
  ```

  Ahora, cada vez que establezcas el atributo `password` en un modelo `User`, se encriptará automáticamente. Además, podrás acceder al atributo `full_name` para obtener el nombre completo del usuario.

Estos son solo algunos aspectos clave de trabajar con modelos y Eloquent ORM en Laravel. Eloquent ofrece muchas más funcionalidades, como consultas en bloque, eventos de modelo, entre otros. Te recomiendo explorar la documentación oficial de Laravel para aprender más sobre estas capacidades.


11. Relaciones polimórficas:
Laravel permite establecer relaciones polimórficas entre modelos, lo que significa que un modelo puede tener una relación con varios tipos de modelos diferentes. Por ejemplo, supongamos que tienes un modelo `Comment` que puede pertenecer tanto a un modelo `Post` como a un modelo `Video`. Puedes establecer una relación polimórfica de la siguiente manera:

```php
class Comment extends Model
{
    public function commentable()
    {
        return $this->morphTo();
    }
}

class Post extends Model
{
    public function comments()
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}

class Video extends Model
{
    public function comments()
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}
```

Ahora puedes acceder a los comentarios de un `Post` o un `Video` de la siguiente manera:

```php
$post = Post::find(1);
$comments = $post->comments;

$video = Video::find(1);
$comments = $video->comments;
```

12. Consultas con relaciones:
Eloquent ORM permite realizar consultas y filtros utilizando las relaciones definidas en los modelos. Por ejemplo, supongamos que tienes un modelo `User` que tiene una relación `hasMany` con el modelo `Post`. Puedes obtener todos los usuarios junto con sus publicaciones utilizando la función `with` de la siguiente manera:

```php
$users = User::with('posts')->get();

foreach ($users as $user) {
    echo "El usuario {$user->name} tiene las siguientes publicaciones: <br>";
    foreach ($user->posts as $post) {
        echo "- {$post->title} <br>";
    }
}
```

De esta manera, se ejecutará una consulta eficiente que obtendrá todos los usuarios junto con sus publicaciones, evitando la necesidad de realizar consultas adicionales para cada usuario.

Estos son solo algunos aspectos adicionales sobre modelos y Eloquent ORM en Laravel. Laravel ofrece una gran cantidad de funcionalidades para trabajar con bases de datos de manera eficiente y sencilla. Te recomiendo explorar más a fondo la documentación oficial de Laravel para aprovechar al máximo estas capacidades.


¡Claro, aquí tienes más información sobre modelos y Eloquent ORM en Laravel!

13. Consultas avanzadas con Eloquent:
Eloquent proporciona una variedad de métodos para realizar consultas avanzadas a la base de datos. Algunos ejemplos son:

- **where**: Permite filtrar los resultados basados en condiciones. Por ejemplo:
  ```php
  $users = User::where('age', '>', 18)->get();
  ```

- **orderBy**: Ordena los resultados en función de una columna específica. Por ejemplo:
  ```php
  $posts = Post::orderBy('created_at', 'desc')->get();
  ```

- **limit**: Limita la cantidad de resultados devueltos. Por ejemplo:
  ```php
  $comments = Comment::limit(10)->get();
  ```

- **join**: Permite unir tablas para realizar consultas más complejas. Por ejemplo:
  ```php
  $users = User::join('posts', 'users.id', '=', 'posts.user_id')
               ->where('posts.is_published', true)
               ->get();
  ```

14. Mutadores y accesores:
Los mutadores y accesores son métodos definidos en un modelo que te permiten modificar y acceder a los valores de los atributos antes de guardarlos en la base de datos o después de obtenerlos de la base de datos. Por ejemplo:

```php
class User extends Model
{
    // Mutador para el atributo 'name'
    public function setNameAttribute($value)
    {
        $this->attributes['name'] = ucfirst($value);
    }

    // Accesor para el atributo 'name'
    public function getNameAttribute($value)
    {
        return strtoupper($value);
    }
}
```

En el ejemplo anterior, el mutador `setNameAttribute` capitaliza la primera letra del nombre antes de guardarlo en la base de datos. El accesor `getNameAttribute` convierte el nombre en letras mayúsculas al obtenerlo de la base de datos.

15. Eventos de modelo:
Laravel proporciona eventos de modelo que se activan en diferentes momentos del ciclo de vida de un modelo, como antes de guardarlo, después de guardarlo, antes de eliminarlo, etc. Puedes aprovechar estos eventos para ejecutar lógica personalizada. Por ejemplo:

```php
class Post extends Model
{
    protected static function boot()
    {
        parent::boot();

        // Evento antes de guardar el modelo
        static::saving(function ($post) {
            // Ejecutar lógica antes de guardar el post
        });

        // Evento después de guardar el modelo
        static::saved(function ($post) {
            // Ejecutar lógica después de guardar el post
        });
    }
}
```

En el ejemplo anterior, se definen los eventos `saving` y `saved` para ejecutar lógica personalizada antes y después de guardar un modelo `Post`.

Espero que esta información adicional sea útil para tu comprensión de los modelos y Eloquent ORM en Laravel.

16. Relaciones entre modelos:
Una de las características más poderosas de Eloquent es la capacidad de establecer relaciones entre modelos. Laravel admite varios tipos de relaciones, como uno a uno, uno a muchos y muchos a muchos. Aquí tienes algunos ejemplos:

- **Relación uno a uno**: Si tienes dos modelos relacionados, como `User` y `Profile`, puedes definir la relación de esta manera:
  ```php
  class User extends Model
  {
      public function profile()
      {
          return $this->hasOne(Profile::class);
      }
  }
  ```
  Y en el modelo `Profile`:
  ```php
  class Profile extends Model
  {
      public function user()
      {
          return $this->belongsTo(User::class);
      }
  }
  ```
  Puedes acceder a la relación de la siguiente manera:
  ```php
  $user = User::find(1);
  $profile = $user->profile;
  ```

- **Relación uno a muchos**: Si tienes dos modelos relacionados, como `User` y `Post`, donde un usuario puede tener muchos posts, puedes definir la relación de esta manera:
  ```php
  class User extends Model
  {
      public function posts()
      {
          return $this->hasMany(Post::class);
      }
  }
  ```
  Y en el modelo `Post`:
  ```php
  class Post extends Model
  {
      public function user()
      {
          return $this->belongsTo(User::class);
      }
  }
  ```
  Puedes acceder a la relación de la siguiente manera:
  ```php
  $user = User::find(1);
  $posts = $user->posts;
  ```

- **Relación muchos a muchos**: Si tienes dos modelos relacionados, como `User` y `Role`, donde un usuario puede tener muchos roles y un rol puede estar asociado con muchos usuarios, puedes definir la relación de esta manera:
  ```php
  class User extends Model
  {
      public function roles()
      {
          return $this->belongsToMany(Role::class);
      }
  }
  ```
  Y en el modelo `Role`:
  ```php
  class Role extends Model
  {
      public function users()
      {
          return $this->belongsToMany(User::class);
      }
  }
  ```
  Puedes acceder a la relación de la siguiente manera:
  ```php
  $user = User::find(1);
  $roles = $user->roles;
  ```

Estos son solo algunos ejemplos de las relaciones que puedes establecer entre modelos en Laravel utilizando Eloquent ORM. Puedes explorar más opciones y configuraciones en la documentación oficial de Laravel.


17. Consultas avanzadas con Eloquent:
Eloquent proporciona una amplia gama de métodos para realizar consultas avanzadas a la base de datos. Estos métodos te permiten realizar operaciones como filtrado, ordenamiento, agrupamiento y más. Aquí tienes algunos ejemplos:

- **Consulta con condición WHERE**: Puedes utilizar el método `where` para agregar condiciones a tu consulta. Por ejemplo:
  ```php
  $users = User::where('age', '>', 18)->get();
  ```

- **Consulta con ordenamiento**: Puedes utilizar el método `orderBy` para ordenar los resultados de tu consulta. Por ejemplo:
  ```php
  $users = User::orderBy('name', 'asc')->get();
  ```

- **Consulta con relación**: Puedes utilizar el método `with` para cargar relaciones relacionadas con tu consulta. Por ejemplo:
  ```php
  $users = User::with('posts')->get();
  ```

- **Consulta con límite y paginación**: Puedes utilizar los métodos `limit` y `paginate` para limitar la cantidad de resultados o implementar la paginación. Por ejemplo:
  ```php
  $users = User::limit(10)->get();
  $users = User::paginate(10);
  ```

- **Consulta con agrupamiento**: Puedes utilizar el método `groupBy` para agrupar los resultados de tu consulta. Por ejemplo:
  ```php
  $users = User::groupBy('age')->get();
  ```

Estos son solo algunos ejemplos de las consultas avanzadas que puedes realizar con Eloquent. Puedes combinar y encadenar múltiples métodos para construir consultas más complejas según tus necesidades.

18. Mutadores y accesores en Eloquent:
Eloquent te permite definir mutadores y accesores en tus modelos para manipular los valores de los atributos antes de guardarlos en la base de datos o antes de mostrarlos. Los mutadores se utilizan para modificar el valor de un atributo antes de guardarlo, mientras que los accesores se utilizan para modificar el valor de un atributo al acceder a él. Aquí tienes un ejemplo:

```php
class User extends Model
{
    public function getNameAttribute($value)
    {
        return ucfirst($value);
    }

    public function setEmailAttribute($value)
    {
        $this->attributes['email'] = strtolower($value);
    }
}
```

En este ejemplo, el mutador `setEmailAttribute` se ejecuta antes de guardar el valor del atributo `email`, lo convierte a minúsculas y lo guarda en la base de datos. El accesor `getNameAttribute` se ejecuta al acceder al valor del atributo `name`, lo convierte a mayúsculas y lo devuelve.

Esto te permite manipular los datos de manera conveniente y consistente antes de que se guarden o se muestren en tu aplicación.

