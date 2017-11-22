---
title: "實施 R 程式碼 （機器學習服務） |Microsoft 文件"
ms.custom: SQL2016_New_Updated
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1f7084d2634d6cce02fcf0e6f945547a535815b2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="operationalize-r-code-machine-learning-services"></a>實施 R 程式碼 （機器學習服務）

資料庫開發人員負責將多項技術整合在一起，並集結所有的結果，讓整個企業一起共用。 資料庫開發人員，適用於應用程式開發人員、 SQL 開發人員和資料科學家，來設計和部署解決方案。

本文摘要說明資料庫開發人員運用使用 SQL Server 的 R 程式碼時要考量的重點。

## <a name="get-started-with-r-code-in-sql-server"></a>開始使用 SQL Server 中的 R 程式碼

傳統上，整合機器學習解決方案的目的在於廣泛的記錄，以支援的效能與整合。 不過，移動到生產環境的 R，並將 Python 程式碼是在 Microsoft 機器學習服務、 更容易，因為程式碼可以執行 SQL Server 中和使用呼叫預存程序。 您可以繼續使用熟悉的工具，而不需要安裝 R 開發環境。 

如需基本語法的詳細資訊，請參閱：

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [在 SQL 中使用 R 程式碼](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

如需如何使用預存程序至生產環境部署的 R 程式碼的範例，請參閱：

+ [資料庫內分析的 SQL 開發人員](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)。

## <a name="optimize-your-r-code"></a>最佳化您的 R 程式碼

當然，轉換 SQL 中的 R 程式碼是某些最佳化事先完成 R 或 Python 程式碼更容易。 這些包括避免資料型別會造成問題，避免不必要的資料轉換，以及將 R 程式碼重寫為單一函數呼叫可以輕鬆地參數化。 如需詳細資訊，請參閱：

+ [R 程式庫和資料類型](r-libraries-and-data-types.md)

+ [轉換使用 R 服務的 R 程式碼](converting-r-code-for-use-in-sql-server.md)

+ [使用 sqlrutils 產生 R 預存程序](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

## <a name="integrate-r-and-python-with-applications"></a>與應用程式整合 R，並將 Python

因為您可以從預存程序啟動機器學習服務，您可以從任何應用程式可以傳送 T-SQL 陳述式和處理結果執行 R 或 Python 指令碼。

例如，您可能會重新訓練排程上的模型使用 「 執行 T-SQL 工作在 Integration Services 中，或使用另一個工作排程器可執行預存程序。

計分是重要的工作，輕鬆地可以自動化，或從外部應用程式啟動。 您定型模型，事先使用 R 或 Python 或預存程序，並將模型儲存至資料表的二進位格式。 然後，此模型可以載入某個變數為預存程序呼叫，從 T-SQL 計分使用其中一個選項的一部分：

+ [即時](../real-time-scoring.md)小批次計分，最佳化
+ 單一資料列計分，用於呼叫從應用程式
+ [原生計分](../sql-native-scoring.md)，從 SQL Server 的快速批次預測，而不需要呼叫 R

本逐步解說提供計分使用批次和單一資料列模式中的預存程序的範例：

+ [端對端 SQL Server 中 R 的資料科學逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

請參閱這些解決方案範本，如需如何整合計分的應用程式中的範例：

+ [零售預測](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [詐騙偵測](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [群集的客戶](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>提升效能和小數位數

雖然已知開放原始碼 R 語言有限制，RevoScaleR 封裝 Api 可以處理大型資料集和受益於多執行緒、 多核心、 多處理序中的資料庫內部計算。

如果您的 R 解決方案使用複雜的彙總，或是牽涉到大型資料集，您可以利用 SQL Server 的高效率記憶體中彙總及資料行存放區索引，讓 R 程式碼處理統計計算和計分。

如需如何在 SQL Server 機器學習中改善效能的詳細資訊，請參閱：

+ [SQL Server R 服務的效能微調](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [最佳化效能的秘訣和訣竅](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>調整其他平台的 R 程式碼，或計算內容

您針對執行的相同 R 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料可用於其他資料來源，例如 Hadoop，和在其他計算內容。

如需支援的 Microsoft R 的平台的詳細資訊，請參閱：

+ [Microsoft R 簡介](https://docs.microsoft.com/r-server/)

+ [瀏覽 RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

如需有關如何最佳化您的 Microsoft R 解決方案，大型資料或多個平台上執行的詳細資訊，請參閱：

+ [寫入區塊處理演算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [計算在 R 中的大型資料](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [開發您自己平行演算法](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

