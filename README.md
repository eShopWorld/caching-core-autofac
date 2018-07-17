# caching-core-autofac

Out of the box, autofac doesnt provide a way to resolve a way to create an instance of a closed generic from an open generic registration, which is problemattic for our strongly typed caching solution.
This package allows this behaviour

#### Further reading

* Please refer to [eshopworld.caching.core](https://github.com/eShopWorld/caching-core) for framework details

### IoC container registration

```c#
public class CacheModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        // default resolution       ICache<T> -> MemoryCache<T>
        // will resolve a closed generic i.e. ICache<Dog> to a MemoryCache<Dog>, using the factory method of the MemoryCacheFactory
        builder.RegisterSource(new CacheRegistrationSource<MemoryCacheFactory>(typeof(ICache<>)));
    }
}
```
