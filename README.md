# Kotlin Cheat Sheet

## Table of Contents

- [Collections](#collections)

## Collections

#### Arrays
```kotlin
val intArray: Array<Int> = arrayOf(1, 2, 3)
val primitiveIntArray: IntArray = intArrayOf(1, 2, 3)
val primitiveDoubleArray: DoubleArray = doubleArrayOf(1, 2, 3)
val primitiveLongArray: LongArray = longArrayOf(1, 2, 3)
val primitiveFloatArray: FloatArray = floatArrayOf(1, 2, 3)

val copyOfArray: Array<Int> = arrayOf(1, 2, 3).copyOf()
val partialCopyOfArray: Array<Int> = arrayOf(1, 2, 3).copyOfRange(0, 2)
```

#### Lists
```kotlin
val intList: List<Int> = listOf(1, 2, 3)
val arrayList: List<Int> = arrayListOf(1, 2, 3)
val emptyList: List<Int> = emptyList()

val listOfNotNull: List<Int> = listOfNotNull(1, null, 3)
```

#### Sets
```kotlin
val set: Set<Int> = setOf(1, 2, 3)
val hashSet: Set<Int> = hashSetOf(1, 2, 3)
val linkedSet: Set<Int> = linkedSetOf(1, 2, 3)

val emptySet: Set<Int> = emptySet()
```

#### Maps
```kotlin
val map: Map<String, Int> = mapOf("foo" to 1, "bar" to 2)
val hashMap: Map<String, Int> = hashMapOf("foo" to 1, "bar" to 2)
val linkedMap: Map<String, Int> = linkedMapOf("foo" to 1, "bar" to 2)

val emptyMap: Map<St­ring, Int> = emptyMap()
```

#### Mutability
```kotlin
val mutableList: MutableList<Int> = mutableListOf(1, 2, 3)
val mutableSet: MutableSet<Int> = mutableSetOf(1)
var mutableMap: MutableMap<String, Int> = mutableMapOf("foo" to 1, "bar" to 2)
```

## Transformers

#### Associate
Returns a map containing key-value pairs created by lambda.
```kotlin
listOf(1, 2, 3).associate { it to "number$it" }   // {1=number1, 2=number2, 3=number3}
```

#### Map
Returns a new collection by transforming all elements from the initial collection.
```kotlin
listOf(1, 2, 3).map { it + 1 }   // [2, 3, 4]
listOf(1, 2, 3).mapIndexed { idx, value -> if (idx == 0) value else value + 1 }   // [1, 3, 4]
listOf(1, 2, 3).mapNotNull { if (it == 1) null else it + 1 }   // [3, 4]
listOf(1, 2, 3).mapIndexedNotNull { idx, value -> if (idx == 0) null else value + 1 }   // [3, 4]
```

#### MapKeys
Transforms all keys from a map, where lamdba return value is the new key of original value.
```kotlin
mapOf("foo" to 1, "bar" to 2).mapKeys { "${it.key}key" }   // {fookey=1, barkey=2}
```

#### MapValues
Transforms all values from a map, where lamdba return value is the new value for the original key.
```kotlin
mapOf("foo" to 1, "bar" to 2).mapValues { it.value + 1 }   // {foo=2, bar=3}
```

#### Sorting
Sorts collection ascending (default) or descending, based on what lambda returns.
```kotlin
listOf(2, 1, 3).sorted()   // [1, 2, 3]
listOf(2, 1, 3).sorted { it }   // [1, 2, 3]
listOf(2, 1, 3).sortedByDescending()   // [3, 2, 1]
listOf(2, 1, 3).sortedWith(Comparator<Int> { x, y -> y - x }   // [1, 2, 3]
```

#### Flattening
Collects (and transforms) elements of all passed collections.
```kotlin
listOf(listOf(1, 2), listOf(3)).flatten()   // [1, 2, 3]
listOf(listOf(1, 2), listOf(3)).flatMap { it }   // [1, 2, 3]
listOf(listOf(1, 2), listOf(3)).flatMap { iterable -> iterable.map { it + 1 } }   // [2, 3, 4]
```

#### Other
```kotlin
listOf(1, 2, 3).reversed()   // [3, 2, 1]
listOf(1, 2, 3).partition { it > 2 })   // Pair([3], [1,2])
listOf(1, 2, 3).slice(1..2)   // [2, 3]
```
