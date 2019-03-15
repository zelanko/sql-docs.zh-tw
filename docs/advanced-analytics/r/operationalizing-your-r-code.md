---
title: 操作 R 程式碼使用預存程序-SQL Server Machine Learning 服務
description: SQL Server 預存程序將提供給任何具有 SQL Server 資料庫的存取權的用戶端應用程式中內嵌 R 語言的程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2b8e6a655ef96da042575a3b48809dbad1215242
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976268"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>操作 SQL Server Machine Learning 服務中使用預存程序的 R 程式碼
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用 R 和 Python 功能時在 SQL Server Machine Learning 服務中，將解決方案移到生產環境中最常見的方法是將程式碼內嵌在預存程序。 本文摘要說明 SQL 開發人員，另尋高就使用 SQL Server 的 R 程式碼時要考量的關鍵要點。

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>部署用於生產環境使用 T-SQL 和預存程序的指令碼

傳統上，使用的資料科學解決方案整合目的在於以支援效能與整合的廣泛記錄。 SQL Server 機器學習服務可簡化這項工作，因為 R 和 Python 程式碼可以在 SQL Server 中執行，並使用預存程序呼叫。 如需將程式碼內嵌在預存程序的運作原理的詳細資訊，請參閱：

+ [快速入門：SQL Server 中的"Hello world"R 指令碼](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

R 程式碼部署至生產環境，使用預存程序的更完整範例，請參閱[教學課程：適用於 SQL 開發人員的 R 資料分析](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>最佳化 SQl R 程式碼的指導方針

轉換 R 程式碼在 SQL 中的是 R 或 Python 程式碼事先完成某些最佳化，您更輕鬆。 這些包括避免會導致問題的資料型別，避免不必要的資料轉換，以及重寫為單一函數呼叫可以輕鬆地參數化的 R 程式碼。 如需詳細資訊，請參閱：

+ [R 程式庫和資料類型](r-libraries-and-data-types.md)
+ [轉換 R 程式碼，在 R Services 中使用](converting-r-code-for-use-in-sql-server.md)
+ [使用 sqlrutils helper 函式](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>整合應用程式中的 R 和 Python

因為您可以從預存程序中執行 R 或 Python，您可以從任何可以傳送的 T-SQL 陳述式並處理結果的應用程式來執行指令碼。 比方說，您可能會重新定型模型在排程上的使用[執行 T-SQL 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)在 Integration Services，或使用另一個工作排程器可執行預存程序。

計分是一項重要的工作，輕鬆地可以自動化，或從外部應用程式已啟動。 您定型模型，事先使用 R 或 Python 或預存程序中，並[二進位格式儲存模型](../tutorials/walkthrough-build-and-save-the-model.md)至資料表。 然後，可以將模型載入某個變數為預存程序呼叫，用於評分從 T-SQL 使用其中一個選項的一部分：

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

開放原始碼 R 語言有已知的限制與大型資料集，雖然[RevoScaleR 封裝 Api](ref-r-revoscaler.md)隨附於 SQL Server Machine Learning 服務可以處理大型資料集，並受益於多執行緒多核心、 多處理序在資料庫內計算。

如果您的 R 解決方案使用複雜的彙總或牽涉到大型資料集，您可以利用 SQL Server 的高效率的記憶體中彙總與資料行存放區索引，然後讓 R 程式碼處理統計計算與評分。

如需如何改善效能，在 SQL Server Machine Learning 中的詳細資訊，請參閱：

+ [SQL Server R Services 的效能微調](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [效能最佳化祕訣和訣竅](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>調整適用於其他平台的 R 程式碼，或計算內容

您針對執行的相同 R 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料可以使用針對其他資料來源，例如透過 HDFS、 Spark，當您使用[獨立伺服器 選項](../install/sql-machine-learning-standalone-windows-install.md)在 SQL Server 安裝程式，或當您安裝非 SQL 品牌的產品，Microsoft Machine Learning 伺服器 (先前稱為**Microsoft R Server**):

+ [Machine Learning Server 文件](https://docs.microsoft.com/r-server/)

+ [RevoScaleR 中探索 R](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [寫入區塊處理演算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [在 R 中的巨量資料運算](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [開發您自己的平行演算法](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

