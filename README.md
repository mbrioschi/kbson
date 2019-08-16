# kbson

# What is this?
This adapter adds BSON support to kotlinx.serialization.

BSON types supported:

- Double	 
- String 
- Array
- Binary 
- ObjectId
- Boolean
- Date
- Symbol
- 32-bit integer
- Long
- Decimal128


## Install

build.gradle.kts
```kotlin
repositories {
    maven { url = uri("https://dl.bintray.com/jershell/generic") }
}

dependencies {
    implementation("com.github.jershell:kbson:0.0.1")
}
```

build.gradle
```groovy
repositories {
    maven { 'https://dl.bintray.com/jershell/generic' }
}

dependencies {
    implementation 'com.github.jershell:kbson:0.0.1'
}
```

# Usage samples
##### Parsing from BSON to a Kotlin object

```kotlin
import kotlinx.serialization.Serializable

@Serializable
data class Simple (
        val valueString: String,
        val valueDouble: Double,
        val valueFloat: Float,
        val valueLong: Long,
        val valueChar: Char,
        val valueBool: Boolean,
        val valueInt: Int
)

val simple = kBson.parse(Simple.serializer(), bsonDocFromMongoJavaDriver)
```

##### Serializing from a Kotlin object to BSON
```kotlin
import kotlinx.serialization.Serializable
import com.github.jershell.kbson.Configuration
import com.github.jershell.kbson.KBson

@Serializable
data class Simple (
        val valueString: String = "default",
        val valueDouble: Double,
        val valueFloat: Float,
        val valueLong: Long,
        val valueChar: Char,
        val valueBool: Boolean,
        val valueInt: Int
)

// Optional configuration
val kBson = KBson(Configuration(encodeDefaults = false))
val bsonDoc = kBson.stringify(Simple.serializer(), simpleModel)
```
###### ps
The default enum class supported like string. You can also override it

# Contributing to kbson
Pull requests and bug reports are always welcome!

To run the tests: ./gradlew check

# Reference links
- http://litote.org/kmongo/ | https://github.com/Litote/kmongo
- https://github.com/Kotlin/kotlinx.serialization
- https://mongodb.github.io/mongo-java-driver/
- Special thanks to: https://github.com/charleskorn/kaml