---
title: 在預存程序中部署 R 程式碼
description: 在 SQL Server 預存程序中內嵌 R 語言程式碼，以便讓任何有權存取 SQL Server 資料庫的用戶端應用程式使用。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/28/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 81cc8f392275093f370a0dda12d1aaf1fca542e5
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288260"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>在 SQL Server 機器學習服務中使用預存程序以便讓 R 程式碼能夠運作
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

在 SQL Server 機器學習服務中使用 R 和 Python 功能時，將解決方案移至實際執行環境的最常見方法是在預存程序中內嵌程式碼。 本文將摘要說明在使用 SQL Server 以便讓 R 程式碼能夠運作時，SQL 開發人員需考慮的重點。

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>使用 T-SQL 和預存程序來部署已準備好用於實際執行環境的指令碼

傳統上，資料科學解決方案的整合意味著要進行大量編碼，以支援效能與整合。 SQL Server 機器學習服務可以簡化此工作，因為 R 和 Python 程式碼可在 SQL Server 中執行，並使用預存程序來呼叫。 如需在預存程序中內嵌程式碼之機制的詳細資訊，請參閱：

+ [在 SQL Server 中建立及執行簡單的 R 指令碼](../tutorials/quickstart-r-create-script.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

如需使用預存程序來將 R 程式碼部署到實際執行環境的更完整範例，請參閱[教學課程：適用於 SQL 開發人員的 R 資料分析](../../machine-learning/tutorials/r-taxi-classification-introduction.md)。

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>將適用於 SQL 的 R 程式碼最佳化的指導方針

如果事先在 R 或 Python 程式碼中進行一些最佳化，則在 SQL 中轉換 R 程式碼會比較容易。 這些最佳化包括避免使用會造成問題的資料類型、避免進行不必要的資料轉換，以及將 R 程式碼重寫為可輕易參數化的單一函式呼叫。 如需詳細資訊，請參閱

+ [R 程式庫和資料類型](r-libraries-and-data-types.md)
+ [使用 sqlrutils 協助程式函式](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>將 R 和 Python 與應用程式整合

由於您可以從預存程序執行 R 或 Python，因此，能夠從任何可傳送 T-SQL 陳述式和處理結果的應用程式執行指令碼。 例如，您可以使用 Integration Services 中的[執行 T-SQL 工作](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)，或使用另一個可執行預存程序的作業排程器，來將模型重新定型。

評分是一項重要工作，可輕易地進行自動化，或從外部應用程式啟動。 您可以事先使用 R 或 Python 或預存程序來將模型定型，並[以二進位格式儲存模型](../tutorials/walkthrough-build-and-save-the-model.md)到資料表。 然後，使用下列其中一個選項，將模型當作預存程序呼叫的一部分載入到變數，以便從 T-SQL 進行評分：

+ 即時評分，已針對小型批次進行最佳化
+ 單一資料列評分，用於從應用程式呼叫
+ [原生評分](../predictions/native-scoring-predict-transact-sql.md)，用於從 SQL Server 進行快速批次預測，而不需呼叫 R

此逐步解說提供在批次和單一資料列模式中使用預存程序進行評分的範例：

+ [適用於 SQL Server 中 R 的端對端資料科學逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)


## <a name="boost-performance-and-scale"></a>提升效能與規模

儘管開放原始碼 R 語言在大型資料集方面存在已知限制，但是 SQL Server 機器學習服務隨附的 [RevoScaleR 套件 API](ref-r-revoscaler.md) 仍能處理大型資料集，並受益於多執行緒、多核心、多處理序的資料庫內部計算。

如果您的 R 解決方案使用複雜的彙總或牽涉到大型資料集，就能運用 SQL Server 的高效率記憶體內部彙總及資料行存放區索引，讓 R 程式碼能夠處理統計計算與評分。

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>針對其他平台或計算內容調整 R 程式碼

當您在 SQL Server 安裝程式中使用[獨立伺服器選項](../install/sql-machine-learning-standalone-windows-install.md)時，或在安裝非 SQL 品牌的產品 Microsoft Machine Learning Server (先前稱為 **Microsoft R Server**) 時，您針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料執行的相同 R 程式碼就能用於其他資料來源 (例如透過 HDFS 的 Spark)：

+ [Machine Learning Server 文件](https://docs.microsoft.com/r-server/) \(英文\)
