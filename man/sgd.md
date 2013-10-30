##### [Logistic Regression (SGD)](https://cwiki.apache.org/confluence/display/MAHOUT/Logistic+Regression)

* http://ashokabhat.wordpress.com/2012/02/13/mahout-and-hadoop-run-the-logistic-regression/
* http://bickson.blogspot.com/2011/01/mahout-on-amazon-ec2-part-2-testing.html
* http://imiloainf.wordpress.com/2011/11/02/mahout-logistic-regression/
* http://jayatiatblogs.blogspot.com/2013/05/running-mahouts-logistic-regression.html
* http://sujitpal.blogspot.com/2012/09/learning-mahout-classification.html
* http://www.cnblogs.com/batys/p/3295942.html
* http://www.datastax.com/dev/blog/apache-mahout-in-datastax-enterprise-building-a-classification-system

#
* http://svn.apache.org/repos/asf/mahout/trunk/examples/src/main/resources/donut.csv
* /workspace/mahout/examples/bin/classify-20newsgroups.sh
* mahout trainlogistic
* mahout runlogistic

#

```bash
curl -o $MAHOUT_WORK/donut.csv \
  -kL http://svn.apache.org/repos/asf/mahout/trunk/examples/src/main/resources/donut.csv
curl -o $MAHOUT_WORK/donut-test.csv \
  -kL http://svn.apache.org/repos/asf/mahout/trunk/examples/src/main/resources/donut-test.csv
mahout trainlogistic \
  --passes 100 --rate 50 --lambda 0.001 --input $MAHOUT_WORK/donut.csv --features 21 \
  --output $MAHOUT_WORK/donut.model --target color --categories 2 --predictors x y xx xy yy a b c --types n n
mahout runlogistic \
  –-input $MAHOUT_WORK/donut-test.csv \
  –-model $MAHOUT_WORK/donut.model –-auc \
  –-scores –-confusion
```

```bash
Usage:
  --quiet
  --input input
  --output output
  --features numFeatures  the number of hashed features to use

  --noBias                don't include a bias term
  --passes passes         the number of times to pass over the input data
  --rate learningRate     the learning rate
  --lambda lambda         the amount of coefficient decay to use

  --types t [t ...]       a list of predictor variable types (numeric, word, or text)
  --predictors p [p ...]  a list of predictor variables
  --categories number     the number of target categories to be considered
  --target target         the name of the target variable
```