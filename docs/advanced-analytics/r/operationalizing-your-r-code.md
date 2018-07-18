---
title: 操作 SQL Server Machine Learning 服務中的 R 程式碼 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 41da5cfe2e545bdcbc59f8d557afc599177c9d5e
ms.sourcegitcommit: f083867f97bb740caa211ca37cb046641172b8c0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38952461"
---
# <a name="operationalize-r-code-machine-learning-services"></a>操作 R 程式碼 （Machine Learning 服務）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

資料庫開發人員負責將多項技術整合在一起，並集結所有的結果，讓整個企業一起共用。 資料庫開發人員與應用程式開發人員、 SQL 開發人員和資料科學家，來設計和部署解決方案。

本文摘要說明資料庫開發人員，另尋高就使用 SQL Server 的 R 程式碼時要考量的關鍵要點。

## <a name="get-started-with-r-code-in-sql-server"></a>開始使用 SQL Server 中的 R 程式碼

傳統上，整合機器學習解決方案的目的在於以支援效能與整合的廣泛記錄。 不過，移至生產環境的 R 和 Python 程式碼是在 SQL Server Machine Learning 服務，更容易，因為程式碼可以執行 SQL Server 中，並使用呼叫預存程序。 您可以繼續使用熟悉的工具，並不需要安裝 R 開發環境。 

如需有關基本語法的詳細資訊，請參閱：

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [在 SQL 中使用 R 程式碼](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

如需如何使用預存程序到生產環境部署 R 程式碼的範例，請參閱：

+ [資料庫內分析適用於 SQL 開發人員](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)。

## <a name="optimize-your-r-code"></a>最佳化您的 R 程式碼

當然，轉換在 SQL 中的 R 程式碼是 R 或 Python 程式碼事先完成某些最佳化，您更輕鬆。 這些包括避免會導致問題的資料型別，避免不必要的資料轉換，以及重寫為單一函數呼叫可以輕鬆地參數化的 R 程式碼。 如需詳細資訊，請參閱：

+ [R 程式庫和資料類型](r-libraries-and-data-types.md)

+ [轉換 R 程式碼，在 R Services 中使用](converting-r-code-for-use-in-sql-server.md)

+ [使用 sqlrutils 產生 R 預存程序](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

## <a name="integrate-r-and-python-with-applications"></a>整合應用程式中的 R 和 Python

因為您可以從預存程序啟動 Machine Learning 服務，您可以從任何可以傳送的 T-SQL 陳述式並處理結果的應用程式來執行 R 或 Python 指令碼。

比方說，您可能會重新定型模型，以定期使用 Integration Services 中的 執行 T-SQL 工作，或使用另一個工作排程器可執行預存程序。

計分是一項重要的工作，輕鬆地可以自動化，或從外部應用程式已啟動。 您定型模型，事先使用 R 或 Python 或預存程序中，並將模型儲存至資料表的二進位格式。 然後，可以將模型載入某個變數為預存程序呼叫，用於評分從 T-SQL 使用其中一個選項的一部分：

+ [即時](../real-time-scoring.md)對於小型批次評分，最佳化
+ 單一資料列評分，從應用程式的呼叫
+ [原生評分](../sql-native-scoring.md)，從 SQL Server 的快速的批次預測，而不需要呼叫 R

本逐步解說提供評分使用批次和單一資料列模式中的預存程序的範例：

+ [端對端資料科學逐步解說適用於 SQL Server 中的 R](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

請參閱這些解決方案範本，如需如何整合應用程式的計分方法的範例：

+ [零售預測](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [詐騙偵測](https://github.com/Microsoft/r-server-fraud-detection)
+ [叢集的客戶](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>提升效能和規模

雖然開放原始碼 R 語言已知有限制，RevoScaleR 封裝 Api 可以處理大型資料集和受益於多執行緒、 多核心、 多處理序在資料庫內計算。

如果您的 R 解決方案使用複雜的彙總或牽涉到大型資料集，您可以利用 SQL Server 的高效率的記憶體中彙總與資料行存放區索引，然後讓 R 程式碼處理統計計算與評分。

如需如何改善效能，在 SQL Server Machine Learning 中的詳細資訊，請參閱：

+ [SQL Server R Services 的效能微調](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [效能最佳化祕訣和訣竅](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>調整適用於其他平台的 R 程式碼，或計算內容

您針對執行的相同 R 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料可用於其他資料來源，例如 Hadoop、 和其他計算內容。

如需 Microsoft R 支援的平台的詳細資訊，請參閱：

+ [Microsoft R 的簡介](https://docs.microsoft.com/r-server/)

+ [瀏覽 RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

如需有關如何最佳化大型資料或多個平台上執行 Microsoft R 解決方案的詳細資訊，請參閱：

+ [寫入區塊處理演算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [在 R 中的巨量資料運算](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [開發您自己的平行演算法](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

