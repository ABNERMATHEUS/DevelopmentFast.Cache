# DevelopmentFast.Cache
Uma biblioteca para ajudar no rápido desenvolvimento para aplicar camada de Cache utilizando Redis, usando Repository Pattern.

<p align="center">
  <img src="https://github.com/ABNERMATHEUS/DevelopmentFast.Cache/blob/master/Logo.svg" width="320" alt="Logo" /></a>
</p>

# Development Fast - Cache


| Package |  Version | Popularity |
| ------- | ----- | ----- |
| `DevelopmentFast.Cache` | [![NuGet](https://img.shields.io/nuget/v/DevelopmentFast.CacheRedis.svg)](https://www.nuget.org/packages/DevelopmentFast.CacheRedis) | [![Nuget](https://img.shields.io/nuget/dt/DevelopmentFast.CacheRedis.svg)](https://www.nuget.org/packages/DevelopmentFast.CacheRedis) |

### What is it ?

<aside>
📌 It is a .NET library with the responsibility to help in the fast development to apply Cache layer using Redis, using Repository Pattern.
</aside>

### Why i created ?

<aside>
📌 To make development easier and save the time I had to configure a cache layer to apply anywhere in the project.

</aside>

### Where is it available ?

<aside>
📌 It is available on .Nuget.org
  
  <br/>
  <a href="https://www.nuget.org/packages/DevelopmentFast.CacheRedis">Nuget Link</a>
    <br/>
  
  `Install-Package DevelopmentFast.CacheRedis -Version 1.0.1`
  
</aside>


### How to use ?


### Dependency and connection injections

```csharp
builder.Services.AddSingleton<IDistributedCache, RedisCache>();
builder.Services.AddStackExchangeRedisCache(x => x.Configuration = "localhost:6379");
```
### Or
```csharp

//Scoped
  services.AddScopedRedisCacheDF(x =>
  {
      x.Configuration = "localhost:6379";
  });

//Transient
  services.AddTransientRedisCacheDF(x =>
  {
      x.Configuration = "localhost:6379";
  });

//Singleton
  services.AddSingletonRedisCacheDF(x =>
  {
      x.Configuration = "localhost:6379";
  });
```


### Constructor

```csharp
private readonly IBaseRedisRepositoryDF _baseRedisRepositoryDF;

public StudentController(IBaseRedisRepositoryDF baseRedisRepositoryDF)
{
    this._baseRedisRepositoryDF = baseRedisRepositoryDF;
}
```

### Create or Update asynchronous

```csharp
var student = new Student("name_student");
await _baseRedisRepositoryDF.CreateOrUpdateAsync<Student>("key_example", student , TimeSpan.FromMinutes(1));
```

### Create or Update synchronous

```csharp
var student = new Student("name_student");
_baseRedisRepositoryDF.CreateOrUpdate<Student>("key_example", student , TimeSpan.FromMinutes(1));
```

### Get asynchronous

```csharp
var student = await _baseRedisRepositoryDF.GetAsync<Student>("key_example");
```

### Get synchronous

```csharp
var student =  _baseRedisRepositoryDF.Get<Student>("key_example");
```

### Remove synchronous

```csharp
_baseRedisRepositoryDF.Remove("key_example");
```

### Remove asynchronous

```csharp
_baseRedisRepositoryDF.RemoveAsync("key_example");
```


### Refresh synchronous

```csharp
_baseRedisRepositoryDF.Refresh("key_example");
```

### Refresh asynchronous

```csharp
_baseRedisRepositoryDF.RefreshAsync("key_example");
```
