---
title: 使用 MLeap 建立和匯出 Spark 機器學習模型
titleSuffix: SQL Server big data clusters
description: 使用 PySpark, 透過 SQL Server big data 叢集 (預覽) 上的 Spark 來定型和建立機器學習模型。 使用 MLeap 匯出, 然後在 SQL Server 中使用 JAVA 為模型評分。
author: RogPodge
ms.author: roliu
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e139e76e5f5f756b57a9366cc896716cda58959
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811215"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>在 SQL Server big data 叢集上建立、匯出和評分 Spark 機器學習模型

下列範例示範如何使用[SPARK ML](https://spark.apache.org/docs/latest/ml-guide.html)建立模型、將模型匯出至[MLeap](http://mleap-docs.combust.ml/), 以及使用[JAVA 語言延伸](../language-extensions/language-extensions-overview.md)模組將模型評分 SQL Server。 這會在 SQL Server 2019 big data 叢集的內容中完成。

下圖說明此範例中所執行的工作:

![使用 spark 訓練分數匯出](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>必要條件

這個範例的所有檔案都位於[https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml)。

若要執行範例, 您也必須具備下列必要條件:

- [SQL Server big data](deploy-get-started.md)叢集

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>使用 Spark ML 進行模型定型

在此範例中, 人口普查資料 (**AdultCensusIncome .csv**) 是用來建立 Spark ML 管線模型。

1. 使用[mleap_sql_test/setup. sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh)檔案從網際網路下載資料集, 並將它放在您的 SQL Server big data cluster 中的 HDFS。 這可讓 Spark 存取它。

1. 然後下載範例筆記本[train_score_export_ml_models_with_spark. ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb)。 從 PowerShell 或 bash 命令列, 執行下列命令以下載筆記本:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   此筆記本包含具有此範例區段之必要命令的儲存格。

1. 在 Azure Data Studio 中開啟筆記本, 然後執行每個程式碼區塊。 如需使用筆記本的詳細資訊, 請參閱[如何在 SQL Server 2019 preview 中使用筆記本](notebooks-guidance.md)。

資料會先讀入 Spark 並分割成定型和測試資料集。 然後, 程式碼會使用定型資料來訓練管線模型。 最後, 它會將模型匯出至 MLeap 組合。

> [!TIP]
> 您也可以在[mleap_sql_test/mleap_pyspark. .py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py)檔案中的筆記本外, 檢查或執行與這些步驟相關聯的 Python 程式碼。

## <a name="model-scoring-with-sql-server"></a>使用 SQL Server 的模型計分

既然 Spark ML 管線模型是通用的序列化[MLeap](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html)組合格式, 您可以在 JAVA 中為模型評分, 而不會有 Spark。 

這個範例會在 SQL Server 中使用[JAVA 語言延伸](../language-extensions/language-extensions-overview.md)模組。 若要對 SQL Server 中的模型進行評分, 您必須先建立 JAVA 應用程式, 將模型載入 JAVA 並對其進行評分。 您可以在[mssql-mleap-app 資料夾](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app)中找到此 JAVA 應用程式的範例程式碼。

建立範例之後, 您可以使用 Transact-sql 呼叫 JAVA 應用程式, 並以資料庫資料表對模型進行評分。 這可以在三個[mleap_sql_test/mleap_sql_tests. .py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py)原始檔中看到。

## <a name="next-steps"></a>後續步驟

如需 big data 叢集的詳細資訊, 請參閱[如何在 Kubernetes 上部署 SQL Server big data](deployment-guidance.md)叢集
