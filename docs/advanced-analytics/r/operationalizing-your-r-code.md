---
title: 使用預存程式來讓 R 程式碼
description: 在 SQL Server 預存程式中內嵌 R 語言程式碼, 讓任何可存取 SQL Server 資料庫的用戶端應用程式使用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: adcac48bc7d90aae5f05a9b671f05e34cc8cf554
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715680"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>在 SQL Server Machine Learning 服務中使用預存程式來讓 R 程式碼
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用 SQL Server Machine Learning 服務中的 R 和 Python 功能時, 將解決方案移至實際執行環境的最常見方法是在預存程式中內嵌程式碼。 本文摘要說明在使用 SQL Server 運用 R 程式碼時, SQL 開發人員所需考慮的重點。

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>使用 T-sql 和預存程式部署已準備好用於生產環境的腳本

傳統上, 資料科學解決方案的整合意味著會進行大量的編碼, 以支援效能與整合。 SQL Server Machine Learning 服務可簡化這項工作, 因為 R 和 Python 程式碼可以在 SQL Server 中執行, 並使用預存程式來呼叫。 如需在預存程式中內嵌程式碼之機制的詳細資訊, 請參閱:

+ [入門SQL Server 中的 "Hello world" R 腳本](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

如需使用預存程式來將 R 程式碼部署到生產環境的更完整[範例, 請參閱教學課程:適用于 SQL 開發人員的 R 資料分析](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>優化 SQl R 程式碼的指導方針

如果在 R 或 Python 程式碼中預先進行一些優化, 則在 SQL 中轉換 R 程式碼會比較容易。 其中包括避免造成問題的資料類型、避免不必要的資料轉換, 並將 R 程式碼重寫為可輕鬆參數化的單一函式呼叫。 如需詳細資訊，請參閱：

+ [R 程式庫和資料類型](r-libraries-and-data-types.md)
+ [轉換 R 程式碼以在 R Services 中使用](converting-r-code-for-use-in-sql-server.md)
+ [使用 sqlrutils helper 函式](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>整合 R 和 Python 與應用程式

由於您可以從預存程式執行 R 或 Python, 因此您可以從任何可傳送 T-sql 語句並處理結果的應用程式來執行腳本。 例如, 您可以使用 Integration Services 中的 [[執行 t-sql](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) ] 工作, 或使用可執行預存程式的另一個作業排程器, 來重新定型模型。

評分是很重要的工作, 可以輕鬆地自動化, 或從外部應用程式啟動。 您可以事先使用 R 或 Python 或預存程式來定型模型, 並將[模型以二進位格式](../tutorials/walkthrough-build-and-save-the-model.md)儲存至資料表。 然後, 您可以使用下列其中一個選項, 將模型當做預存程序呼叫的一部分載入變數中, 以便從 T-sql 進行評分:

+ [即時評分, 針對小型批次優化
+ 單一資料列評分, 用於從應用程式呼叫
+ [原生評分](../sql-native-scoring.md), 用於從 SQL Server 的快速批次預測, 而不需要呼叫 R

本逐步解說提供在批次和單一資料列模式中使用預存程式進行評分的範例:

+ [SQL Server 中 R 的端對端資料科學逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

如需如何在應用程式中整合計分的範例, 請參閱下列解決方案範本:

+ [零售預測](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [詐騙偵測](https://github.com/Microsoft/r-server-fraud-detection)
+ [客戶群集](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>提升效能和規模

雖然開放原始碼 R 語言對於大型資料集有已知的限制, 但 SQL Server Machine Learning 服務所包含的[RevoScaleR 封裝 api](ref-r-revoscaler.md) , 可以在大型資料集上運作, 並受益于多執行緒、多核心、多進程資料庫內計算。

如果您的 R 解決方案使用複雜的匯總, 或牽涉到大型資料集, 您可以利用 SQL Server 高效率的記憶體內部匯總和資料行存放區索引, 並讓 R 程式碼處理統計計算和計分。

如需如何在 SQL Server Machine Learning 中改善效能的詳細資訊, 請參閱:

+ [SQL Server R Services 的效能微調](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [效能優化秘訣和訣竅](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>調整其他平臺或計算內容的 R 程式碼

您針對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料執行的相同 R 程式碼可以用於其他資料來源, 例如 Spark over HDFS、當您使用 SQL Server 安裝程式中的 [[獨立伺服器] 選項](../install/sql-machine-learning-standalone-windows-install.md)時, 或安裝非 SQL 品牌的產品時, Microsoft Machine Learning伺服器 (先前稱為**Microsoft R server**):

+ [Machine Learning Server 檔](https://docs.microsoft.com/r-server/)

+ [探索 R 至 RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [寫入區塊化演算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [以 R 計算海量資料](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [開發您自己的平行演算法](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

