---
title: 匯出 MLeap 使用 Spark ML 模型
titleSuffix: SQL Server big data clusters
description: 了解如何匯出 Spark 機器學習服務模型與 MLeap。
author: lgongmsft
ms.author: shivprashant
ms.reviewer: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 7d62cc32be569bec6e1560b4b712ff0ac9cba553
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803063"
---
# <a name="export-spark-machine-learning-models-with-mleap"></a>匯出 Spark 機器學習服務模型與 MLeap

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

典型的機器學習案例牽涉到在 Spark 上的模型訓練和評分 Spark 之外。 匯出的可攜式格式的模型，使它可以使用外部 Spark。 [MLeap](https://github.com/combust/mleap)是一種這類模型交換格式。 它可讓 Spark 機器學習服務管線和模型，以匯出為可移植的格式和用於 JVM 為基礎系統`Mleap`執行階段。

本指南示範如何將匯出使用 Mleap spark 模型。 步驟摘要如下，並使用下一節中的程式碼的詳細。

1. 開始建立 Spark 的模型。 為此用途**定型集和建立機器學習服務模型與 Spark[這裡。](train-and-create-machinelearning-models-with-spark.md)**
2. 我們將在下一個步驟**匯入 training\test 資料和模型**
3. **匯出為模型`Mleap`配套**。 此匯出的套件組合現在可用來評分 spark 外部使用。
4. 若要驗證，我們將匯入`Mleap`再次配套後，並使用它來在 Spark 中評分。

## <a name="step-1---start-by-creating-a-spark-model"></a>步驟 1-建立的 Spark 模型開始
執行[定型集和建立機器學習服務模型與 Spark](train-and-create-machinelearning-models-with-spark.md)建立訓練/測試集和模型，並保存到 HDFS 儲存體。 模型應該匯出為`AdultCensus.mml`下`spark_ml`目錄。

## <a name="step-2---import-the-trainingtest-data-and-the-model"></a>步驟 2-匯入 training\test 資料和模型

步驟 1 建立`AdultCensus.mml`，這是 spark 模型。 

在此步驟中，匯入 spark 模型。

```python
import mleap.pyspark
from mleap.pyspark.spark_support import SimpleSparkSerializer
from pyspark.ml import PipelineModel

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

print("load pyspark model from hbfs")
model = PipelineModel.load(model_fs)
print("Model is " , model)
print("Model stages", model.stages)
```

## <a name="step-3---export-the-model-as-mleap-bundle"></a>步驟 3-匯出模型`Mleap`套件組合

將 Spark 模型匯出為可攜式`Mleap`模型，並將它保存在本機儲存體。 張貼此步驟中，模型在可攜式`Mleap`格式化，並可以使用外部 Spark。

```python
import os

#Get the train and test datasets

# Write the train and test data sets to intermediate storage

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train = spark.read.orc(train_data_path)
test = spark.read.orc(test_data_path)

print("train: ({}, {})".format(train.count(), len(train.columns)))
train.printSchema()

print("test: ({}, {})".format(test.count(), len(test.columns)))
test.printSchema()

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# remove an old model file, if needed.
try:
    os.remove(model_file)
except OSError:
    pass

model_file_path = "jar:file:{}".format(model_file)
model.serializeToBundle(model_file_path, model.transform(train))

```

保存`Mleap`配套從本機 hdfs

```python
print("persist the mleap bundle from local to hdfs")
from subprocess import Popen, PIPE
proc = Popen(["hadoop", "fs", "-put", "-f", model_file, os.path.join("/spark_ml", model_name_export)], stdout=PIPE, stderr=PIPE)
s_output, s_err = proc.communicate()
if(s_err):
    print("Error when storing to HDFS")
```

## <a name="step-3---validate-by-importing-the-mleap-bundle-and-scoring-in-spark"></a>步驟 3-匯入來驗證`Mleap`組合和 Spark 中的計分
在步驟 2 中，我們已匯出模型移植至`Mleap`可以使用外部 Spark 的格式。 在此步驟中，我們匯入`Mleap`在 Spark 中序列化，並在測試集分數的 Spark 中使用它。
   
```python
model_deserialized = PipelineModel.deserializeFromBundle(model_file_path)
print("The deserialized model is ", model_deserialized)
print("The deserialized model stages are", model_deserialized.stages)

from pyspark.ml.evaluation import BinaryClassificationEvaluator

# make prediction
pred = model_deserialized.transform(test)


# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Results of using the model score test set")
print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```

## <a name="references"></a>參考

* [開始使用 PySpark notebook](notebooks-guidance.md)
* [定型集和使用 Spark 建立機器學習服務模型](train-and-create-machinelearning-models-with-spark.md)
