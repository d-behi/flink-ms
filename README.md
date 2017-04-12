# flink-ms
Serving layer for large machine learning models on Apache Flink

Apache Flink [1] is a unified batch and stream processing framework for big data, which is often referred
to as the 4th generation of big data frameworks, offering real time stream processing as well as
batch processing on top of its streaming dataflow engine [2]. Its dedicated support for iterative computations
including bulk and delta iterations [2] makes it ideal for many scalable machine learning
applications. The machine learning library of Flink, called FlinkML [3] is a relatively new effort in the
Flink community, with a vision to add scalable machine learning algorithms which are easy to use and
with minimal glue code in end-to-end machine learning systems [3].
One of the critical components in machine learning applications in big data systems is the deployment
of large models, serving different applications which uses this model for predictions. The ability
to update the models with the newly observed data after the initial training is also important.
Often big data frameworks are used only for the training of the models, and then it is moved to the
serving layer, which typically resides outside of the big data framework. Incremental updates to the
model is often not performed, instead a retraining of the entire model is carried out in scheduled
frequencies. This is not ideal for many applications, and the research community is now trying to address
this issue to have end-to-end machine learning systems within the big data frameworks, which
can perform training and updating of the models, serving external applications, and perform retraining
as the quality decreases beyond a threshold.

Velox [4] try to address this issue in Berkeley Data Analytics Stack (BDAS) by proposing a model manager
for online updates and triggering the retraining of models when required, and a model predictor
with a low-latency up-to-date prediction interface for serving different applications which uses this
model. How ever the big data platform in consideration - Apache Spark, is only used in the initial
training and batch retraining of the model. Other components reside outside of Apache Spark.
Parameter servers [5] used in distributed machine learning is another important research in this context.
They provide globally shared model parameters stored across server nodes which can be accessed
asynchronously. Parameter servers are used heavily for large scale machine learning model
training, how ever they have not been explored in the context of serving large machine learning
models.

The proposed Queryable state [6] feature in Apache Flink (To be released in Version 1.2 [7]), is also
promising in this context. “Flink offers state abstractions for user functions in order to guarantee
fault-tolerant processing of streams. The goal of Queryable State is to expose this state outside of
Flink by supporting queries against the partitioned key value state” [6].
As the machine learning efforts on Apache Flink grows, many applications will be benefitted to have
an end-to-end, machine learning model deployment and serving layer on top of Flink. This thesis aims
to take motivation from the mentioned literatures and design a serving layer for large machine learning
models, on top of Apache Flink.

[1] Apache Flink, Accessed on 28/12/2016, https://flink.apache.org
[2] P. Carbone, A. Katsifodimos, S. Ewen, V. Markl, S. Haridi, and K. Tzoumas, Apache flink: Stream and batch processing in
a single engine, Data Engineering, p. 28, 2015.
[3] Apache FlinkML, Accessed on 28/12/2016, https://ci.apache.org/projects/flink/flink-docs-release-1.2/dev/libs/ml
[4] D. Crankshaw, P. Bailis, J. E. Gonzalez, H. Li, Z. Zhang, M. J. Franklin, A. Ghodsi, and M. I. Jordan. The missing piece in
complex analytics: Low latency, scalable model management and serving with velox. In Conference on Innovative Data
Systems Research (CIDR), 2015.
[5] M. Li, D. G. Andersen, J. W. Park, A. Ahmed, V. Josifovski, J. Long, E. J. Shekita, and B.-Y. Su. Scaling distributed machine
learning with the parameter server. In OSDI, pages 583–598, 2014.
[6] Add Support for Queryable state, Accessed on 28/12/2016, https://issues.apache.org/jira/browse/FLINK-3779
[7] Apache Flink Release and Feature Plan, Accessed on 28/12/2016
https://cwiki.apache.org/confluence/display/FLINK/Flink+Release+and+Feature+Plan
