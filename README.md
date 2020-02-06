# Kotlin Cheat Sheet

## Table of Contents

- [Collections](#collections)

### Collections

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
val map: Map<String, Int> = hashMapOf("foo" to 1, "bar" to 2)
val map: Map<String, Int> = linkedMapOf("foo" to 1, "bar" to 2)

val emptyMap: Map<St­ring, Int> = emptyMap()
```

#### Mutability
```kotlin
val mutableList: MutableList<Int> = mutableListOf(1, 2, 3)
val mutableSet: MutableSet<Int> = mutableSetOf(1)
var mutableMap: MutableMap<String, Int> = mutableMapOf("foo" to 1, "bar" to 2)
```
