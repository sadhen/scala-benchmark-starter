# A Benchmark Starter for Scala Project

## Example: The Magic `-opt:l:inline` and `-opt-inline-from`

see https://github.com/scala/scala-dev/issues/81

```
sbt clean 'project benchmark' 'set scalaVersion := "2.11.12"' 'jmh:run -f 1 -i 20 -wi 20 -t 1 Richards'
[info] Benchmark      Mode  Cnt     Score    Error  Units
[info] Richards.run  thrpt   20  7464.953 ± 65.303  ops/s

sbt clean 'project benchmark' 'set scalaVersion := "2.12.6"' 'jmh:run -f 1 -i 20 -wi 20 -t 1 Richards'
[info] Benchmark      Mode  Cnt     Score    Error  Units
[info] Richards.run  thrpt   20  6623.674 ± 51.901  ops/s

sbt clean 'project benchmark' 'set scalaVersion := "2.12.6"' 'set scalacOptions in ThisBuild ++= Seq("-opt:l:inline", "-opt-inline-from")' 'jmh:run -f 1 -i 20 -wi 20 -t 1 Richards'
[info] Benchmark      Mode  Cnt     Score    Error  Units
[info] Richards.run  thrpt   20  7456.257 ± 23.585  ops/s
```