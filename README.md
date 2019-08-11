# SparkExamples
#spark examples using scala
#mapPartitions() can be used as an alternative to map() & foreach(). 
#mapPartitions() is called once for each Partition unlike map() & foreach() which is called for each element in the RDD. 
#whenever you see that some operations are common to all elements,you could do it once and could process all of them, it's better to go #with mapPartitions/mapPartitionsWithIndex

#MapPartitionsWithIndex
val rdd1=sc.parallelize(Seq("suraj","rahul","siddu"))
val res =   rdd1.mapPartitionsWithIndex{
(index, iterator) => {
val data = iterator.toList
data.map(x => x + " in  partition ->" + index).iterator
}
}
res.collect()

output:
------------------------------
suraj in partition ->2
rahul in partition ->5 
siddu in partition ->7

#MapPartitions
val parallel = sc.parallelize(1 to 9, 3)
def func(iter:Iterator[(Int)]):Iterator[Int]={
  var sum=1
  while(iter.hasNext){
    var data=iter.next
    sum += data
  }
 return Iterator(sum)
}
parallel.mapPartitions(func).collect()

output:
------------------------
7, 16, 25
                                        
