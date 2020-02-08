# Kotlin Cheat Sheet

## Table of Contents

1. [Collections](#collections)
    1. [Arrays](#arrays)
    1. [Lists](#lists)
    1. [Sets](#sets)
    1. [Maps](#maps)
    1. [Mutability](#mutability)
1. [Transformers](#transformers)
    1. [Associate](#associate)
    1. [Map](#map)
    1. [MapKeys](#mapkeys)
    1. [MapValues](#mapvalues)
    1. [Sorting](#sorting)
    1. [Flattening](#flattening)
1. [Aggregators](#aggregators)
    1. [Fold](#fold)
    1. [Reduce](#reduce)
    1. [Grouping](#grouping)
    1. [Chunked](#chunked)


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

val emptyMap: Map<String, Int> = emptyMap()
```

#### Mutability
```kotlin
val mutableList: MutableList<Int> = mutableListOf(1, 2, 3)
val mutableSet: MutableSet<Int> = mutableSetOf(1)
var mutableMap: MutableMap<String, Int> = mutableMapOf("foo" to 1, "bar" to 2)
```

## Transformers

```kotlin
listOf(1, 2, 3).reversed()   // [3, 2, 1]
listOf(1, 2, 3).partition { it > 2 }   // Pair([3], [1,2])
listOf(1, 2, 3).slice(1..2)   // [2, 3]
```

#### Associate
Returns a map containing key-value pairs created by lambda.
```kotlin
listOf(1, 2, 3).associate { "key$it" to "val$it" }   // {key1=val1, key2=val2, key3=val3}
listOf(1, 2, 3).associateWith { "val$it" }   // {1=val1, 2=val2, 3=val3}
listOf(1, 2, 3).associateBy { "key$it" }   // {key1=1, key2=2, key3=3}
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
listOf(2, 1, 3).sortedWith(Comparator { x, y -> x - y })   // [1, 2, 3]
```

#### Flattening
Collects (and transforms) elements of all passed collections.
```kotlin
listOf(listOf(1, 2), listOf(3)).flatten()   // [1, 2, 3]
listOf(listOf(1, 2), listOf(3)).flatMap { it }   // [1, 2, 3]
listOf(listOf(1, 2), listOf(3)).flatMap { iterable -> iterable.map { it + 1 } }   // [2, 3, 4]
```

## Aggregators

```kotlin
listOf(1, 2, 3).count()   // 3
listOf(1, 2, 3).count { it == 3 }  // 1

listOf(1, 2, 3).average()   // 2.0

listOf(1, 2, 3).max()   // 3
listOf(1, 2, 3).maxBy { it * 5 }   // 3

listOf(1, 2, 3).min()   // 1
listOf(1, 2, 3).minBy { it * 5 }   // 1

listOf(1, 2, 3).sum()   // 6
listOf(1, 2, 3).sumBy { if (it == 3) 6 else it }   // 9 (1+2+6)
listOf(1, 2, 3).sumByDouble { it.toDouble() + 1.0 }   // 9 (2+3+4)
```

#### Fold
Accumulates values starting with initial supplied value and applying operation from left to right (default) or right to left (foldRight).
```kotlin
listOf(1, 2, 3).fold(5) { accumulator, value -> accumulator + value }   // 11 (5+1+2+3)
listOf(1, 2, 3).foldIndexed(5) { idx, accumulator, value ->
   if (idx == 0) accumulator else accumulator + value   // 10 (5+2+3)
}

listOf(1, 2, 3).foldRight(5) { value, accumulator -> accumulator + value }   // 11 (5+3+2+1)
listOf(1, 2, 3).foldRightIndexed(5) { idx, value, accumulator ->
   if (idx == 0) accumulator else accumulator + value   // 8 (5+2+1)
}
```

#### Reduce
Accumulates values starting with first value and applying operation from left to right (default) or right to left (foldRight).
```kotlin
listOf(1, 2, 3).reduce { accumulator, value -> accumulator + value }   // 6 (1+2+3)
listOf(1, 2, 3).reduceIndexed { idx, accumulator, value ->
   if (idx == 0) accumulator else accumulator + value   // 5 (2+3)
}

listOf(1, 2, 3).reduceRight { value, accumulator -> accumulator + value }   // 6 (3+2+1)
listOf(1, 2, 3).reduceRightIndexed { idx, value, accumulator ->
   if (idx == 0) accumulator else accumulator + value   // 5 (3+2)
}
```

#### Grouping
Uses value returned from (first) lambda to group elements of the collection.
```kotlin
listOf(1, 2, 3).groupBy { "key" }   // {key=[1, 2, 3]}
listOf(1, 2, 3).groupBy({ "key$it" }) { it + 1 }   // {key1=[2], key2=[3], key3=[4]}

listOf(1, 2, 3).groupByTo(mutableMapOf(), { it }) { it + 10 }   // {1=[11], 2=[12], 3=[13]}
```

#### Chunked
Splits this collection into a list of lists, each not exceeding the given size.
```kotlin
listOf("one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten")
    .chunked(3)   // [[one, two, three], [four, five, six], [seven, eight, nine], [ten]]
```
