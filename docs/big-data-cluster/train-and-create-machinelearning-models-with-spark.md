---
title: 使用 Spark 的訓練/建立 ML 模型
titleSuffix: SQL Server big data clusters
description: 使用 PySpark 來訓練及 SQL Server 的巨量資料叢集 （預覽） 上建立 Spark 機器學習服務模型。
author: lgongmsft
ms.author: lgong
ms.manager: craigg
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 348749b038b97138c4a6c85fd2f56b45b85c5d60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822928"
---
# <a name="train-and-create-machine-learning-models-with-spark"></a>訓練及建立 Spark 機器學習服務模型

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在巨量資料的 SQL Server 叢集的 Spark 可讓人工智慧和機器學習服務。 此範例會示範如何訓練機器學習模型使用 Python 中使用資料的 Spark (PySpark) 儲存在 HDFS。 

此範例是有可用的程式碼片段的逐步解說指南，從 Azure Data Studio Notebook 和每個資料格執行一個步驟一次。 如需如何從 notebook 與 Spark 連接的詳細資訊，請參閱[這裡](notebooks-guidance.md)

在範例中︰

1. 開始使用**了解資料和所需的預測**
2. **將資料上傳至 HDFS 和準備資料**建立模型
3. **選取要使用的功能**
4. **將資料分割為訓練和測試集**
5. 匯集了**ml 管線和建置模型**
6. 使用建立的模式**做出預測**
7. 最後一個步驟中，**保存於稍後使用建立的模型**。

E2E 機器學習服務牽涉到數個額外的步驟、 例如、 資料探索、 功能選取項目和主體元件分析、 模型選取項目。 為求簡單明瞭這裡忽略其中許多步驟。

## <a name="step-1---understanding-the-data-and-prediction-desired"></a>步驟 1-了解資料和所需的預測

這個範例會使用收入資料成人人口普查[此處]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv )。 在  `AdultCensusIncome.csv`、 每個資料列都代表收入範圍和其他特性，例如 age，每週時數教育、 職業等等的指定成人。 建立模型，如果可預測的收入範圍。 會採用存留期和小時每週做為特徵的模型，並將其預測如果收入 > 50k 或 < 50 k。 

## <a name="step-2---upload-the-data-to-hdfs-and-basic-explorations-on-data"></a>步驟 2-將資料上傳至 HDFS 和基本資料上的探勘
從 Azure Data Studio 連接到 HDFS/Spark 閘道，並建立名為的目錄`spark_ml`下 HDFS。 下載[AdultCensusIncome.csv]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv )您的本機電腦和上的傳至 HDFS。 上傳`AdultCensusIncome.csv`至您所建立的資料夾。


現在，撰寫一些程式碼。 您可以複製下列程式碼，並將它貼在個別的儲存格的 Azure Data Studio 中的筆記本。 

下列程式碼會讀取到 Spark 資料框架的 CSV 檔案。 進一步，它會計算的資料列和資料行數目，並顯示載入的資料。

```python
datafile = "/spark_ml/AdultCensusIncome.csv"

#Read the data to a spark data frame.
data_all = spark.read.format('csv').options(header='true', inferSchema='true', ignoreLeadingWhiteSpace='true', ignoreTrailingWhiteSpace='true').load(datafile)
print("Number of rows: {},  Number of coulumns : {}".format(data_all.count(), len(data_all.columns)))

#Replace "-" with "_" in column names
columns_new = [col.replace("-", "_") for col in data_all.columns]
data_all = data_all.toDF(*columns_new)

#Print Schema and show top 5 row
data_all.printSchema() 
data_all.show(5)
```

## <a name="step-3---select-features-to-use"></a>步驟 3-選取要使用的功能

在此步驟中，使用下列兩個詞彙
1. `Label`    -是指要預測的值。 這表示為資料中的資料行。  
2. `Features` -是指要預測的資料中的特性。 也請參考一些時間為 `predictors` 

在此範例中`Label`，為**收入**資料行。 為了簡單起見，請選擇**年齡**並**hours_per_week**做為`Features`。 事實上功能會選擇藉由套用一些相互關聯的技巧，來了解什麼最能描述預測的標籤。

```python
# Choose feature columns and the label column.
label = "income"
xvars = ["age", "hours_per_week"] #all numeric

print("label = {}".format(label))
print("features = {}".format(xvars))

select_cols = xvars
select_cols.append(label)
data = data_all.select(select_cols)

```

## <a name="step-4---split-as-training-and-test-set"></a>步驟 4-分割為訓練和測試集

來定型模型和 25%，以評估模型的其餘部分使用的資料列的 75%。 此外，保存定型和測試資料集，HDFS 儲存體。 步驟並非必要，但要示範顯示儲存及載入以 ORC 格式。 其他格式，例如`Parquet`也可以使用。

張貼您應該會看到此步驟中建立具有名稱 AdultCensusIncomeTrain 和 AdultCensusIncomeTest 的兩個目錄

```python

# Split data into train and test.
train, test = data.randomSplit([0.75, 0.25], seed=123)

print("train ({}, {})".format(train.count(), len(train.columns)))
print("test ({}, {})".format(test.count(), len(test.columns)))

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train.write.mode('overwrite').orc(train_data_path)
test.write.mode('overwrite').orc(test_data_path)
print("train and test datasets saved to {} and {}".format(train_data_path, test_data_path))

```

## <a name="step-5---put-together-a-pipeline-and-build-a-model"></a>步驟 5-匯集了管線和建立模型
[Spark ML 管線](https://spark.apache.org/docs/2.3.1/ml-pipeline.html)允許順序做為工作流程的所有步驟，並讓您更輕鬆地試驗不同的演算法和其參數。 下列程式碼先建構階段，並接著將這些階段一起放在 Ml 管線。  LogisticRegression 用來建立模型。

```python
from pyspark.ml import Pipeline, PipelineModel
from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler
from pyspark.ml.classification import LogisticRegression

reg = 0.1
print("Using LogisticRegression model with Regularization Rate of {}.".format(reg))

# create a new Logistic Regression model.
lr = LogisticRegression(regParam=reg)

dtypes = dict(train.dtypes)
dtypes.pop(label)

si_xvars = []
ohe_xvars = []
featureCols = []
for idx,key in enumerate(dtypes):
    if dtypes[key] == "string":
        featureCol = "-".join([key, "encoded"])
        featureCols.append(featureCol)
        
        tmpCol = "-".join([key, "tmp"])
        si_xvars.append(StringIndexer(inputCol=key, outputCol=tmpCol, handleInvalid="skip")) #, handleInvalid="keep"
        ohe_xvars.append(OneHotEncoder(inputCol=tmpCol, outputCol=featureCol))
    else:
        featureCols.append(key)

# string-index the label column into a column named "label"
si_label = StringIndexer(inputCol=label, outputCol='label')

# assemble the encoded feature columns in to a column named "features"
assembler = VectorAssembler(inputCols=featureCols, outputCol="features")

```

現在，匯集了管線。 

```python
# put together the pipeline
stages = []
stages.extend(si_xvars)
stages.extend(ohe_xvars)
stages.append(si_label)
stages.append(assembler)
stages.append(lr)
pipe = Pipeline(stages=stages)
print("Pipeline Created")

```

現在，建立管線時，請使用它來定型模型。

```python
# train the model
model = pipe.fit(train)
print("Model Trained")
print("Model is ", model)
print("Model Stages", model.stages)

```

## <a name="step-6---predict-using-the-model-and-evaluate-the-model-accuracy"></a>步驟 6-使用模型進行預測和評估模型的精確度
下列程式碼會使用測試資料集，來預測使用上述步驟中建立之模型的結果。 它會測量與模型的精確度`areaUnderROC`和`areaUnderPR`計量。

```python
from pyspark.ml.evaluation import BinaryClassificationEvaluator
# make prediction
pred = model.transform(test)

# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```


## <a name="step-7---persist-the-models-to-hdfs"></a>步驟 7-保存到 HDFS 的模型
最後，保存在 HDFS 中的模型，以供稍後使用。 張貼此步驟中建立的模型會儲存為 /spark_ml/AdultCensus.mml

```python
##NOTE: by default the model is saved to and loaded from path

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

model.write().overwrite().save(model_fs)
print("saved model to {}".format(model_fs))

# load the model file (from dbfs)
model2 = PipelineModel.load(model_fs)
assert str(model2) == str(model)
print("loaded model from {}".format(model_fs))
```

## <a name="next-steps"></a>後續步驟

如需有關如何開始使用 PySpark notebook 的詳細資訊，請參閱 <<c0> [ 如何使用 notebook](notebooks-guidance.md)。