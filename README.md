# spark-stringmetric

Making similarity functions and phonetic algorithms readily available for fuzzy matching analyses in Spark.

## Project Setup

Update your `build.sbt` files to import the libraries.

```
libraryDependencies += "org.apache.commons" % "commons-text" % "1.1"
libraryDependencies += "mrpowers" % "spark-stringmetric" % "2.2.0_0.1.0"
```

## SimilarityFunctions

* `cosine_distance`
* `fuzzy_score`
* `hamming`
* `jaccard_similarity`
* `jaro_winkler`

Import the functions.

```scala
import com.github.mrpowers.spark.stringmetric.SimilarityFunctions._
```

Here's an example on how to use the `jaccard_similarity` function.

Suppose we have the following `sourceDF`:

```
+-------+-------+
|  word1|  word2|
+-------+-------+
|  night|  nacht|
|context|contact|
|   null|  nacht|
|   null|   null|
+-------+-------+
```

Let's run the `jaccard_similarity` function.

```scala
val actualDF = sourceDF.withColumn(
  "w1_w2_jaccard",
  jaccard_similarity(col("word1"), col("word2"))
)
```

We can run `actualDF.show()` to view the `w1_w2_jaccard` column that's been appended to the DataFrame.

```
+-------+-------+-------------+
|  word1|  word2|w1_w2_jaccard|
+-------+-------+-------------+
|  night|  nacht|         0.43|
|context|contact|         0.57|
|   null|  nacht|         null|
|   null|   null|         null|
+-------+-------+-------------+
```

## PhoneticAlgorithms
