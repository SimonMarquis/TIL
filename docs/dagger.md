---
title: 🗡️ Dagger
---

### Binding extension functions

```kotlin
@Module
abstract class RepositoryModule {

    @Binds
    abstract fun RepositoryImpl.bind(): Repository

    @Binds
    abstract fun @receiver:MyQualifier RepositoryImpl.bind(): Repository

}
```

```kotlin
@Module
interface RepositoryModule {

    @get:Binds
    val RepositoryImpl.bind: Repository

}
```

[🔗](https://www.zacsweers.dev/dagger-party-tricks-extension-functions/)

### Coroutines provider

```kotlin
@Qualifier
annotation class Dispatcher(val type: Type) {
    enum class Type { Default, IO, Main, MainImmediate, Unconfined }
}


@Module @InstallIn(SingletonComponent::class)
object CoroutinesModule {

    @Provides @Dispatcher(Main)
    fun main(): CoroutineDispatcher = Dispatchers.Main

    @Provides @Dispatcher(MainImmediate)
    fun mainImmediate(): CoroutineDispatcher = Dispatchers.Main.immediate

    @Provides @Dispatcher(Default)
    fun default(): CoroutineDispatcher = Dispatchers.Default

    @Provides @Dispatcher(IO)
    fun io(): CoroutineDispatcher = Dispatchers.IO

    @Provides @Dispatcher(Unconfined)
    fun unconfined(): CoroutineDispatcher = Dispatchers.Unconfined

    @Provides
    fun provider(): CoroutineDispatcherProvider = object : CoroutineDispatcherProvider {}

}

interface CoroutineDispatcherProvider {
    fun main(): CoroutineDispatcher = Main
    fun immediate(): CoroutineDispatcher = Main.immediate
    fun default(): CoroutineDispatcher = Default
    fun io(): CoroutineDispatcher = IO
    fun unconfined(): CoroutineDispatcher = Unconfined
}

fun CoroutineDispatcher.asDispatcherProvider() = object : DispatcherProvider {
    override fun main(): CoroutineDispatcher = this@asDispatcherProvider
    override fun mainImmediate(): CoroutineDispatcher = this@asDispatcherProvider
    override fun default(): CoroutineDispatcher = this@asDispatcherProvider
    override fun io(): CoroutineDispatcher = this@asDispatcherProvider
    override fun unconfined(): CoroutineDispatcher = this@asDispatcherProvider
}
```

### Dagger types with JvmSuppressWildcards

```kotlin
package dagger

typealias List<T> = @JvmSuppressWildcards kotlin.collections.List<T>
typealias Set<T> = @JvmSuppressWildcards kotlin.collections.Set<T>
typealias Map<K, V> = @JvmSuppressWildcards kotlin.collections.Map<K, V>
```

### Extensions for Lazy & Provider

```kotlin
package dagger

import kotlin.reflect.KProperty

operator fun <T> Provider<T>.getValue(thisRef: Any?, property: KProperty<*>): T = get()
operator fun <T> Lazy<T>.getValue(thisRef: Any?, property: KProperty<*>): T = get()

class Repository @Inject constructor(
    api: dagger.Lazy<Api>,
) {
    private val api by api
}
```

### Private dependencies

```kotlin
@Qualifier private annotation class InternalApi

@Module
object NetworkModule {

    @Provides @InternalApi 
    fun provideClient(): OkHttpClient = ...

    @Provides
    fun provideRetrofit(@InternalApi client: Lazy<OkHttpClient>): Retrofit = ...

}
```

[🔗](https://www.zacsweers.dev/dagger-party-tricks-private-dependencies/)
