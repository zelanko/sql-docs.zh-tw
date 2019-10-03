---
title: 使用 Resource Governor 管理 Python 和 R 工作負載
description: 瞭解如何使用 Resource Governor 來管理 SQL Server Machine Learning 服務中適用于 Python 和 R 工作負載的 CPU、實體 IO 和記憶體資源配置。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/02/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9000ab8bb15e8f9910b8b780aa38d134fa984032
ms.sourcegitcommit: af5e1f74a8c1171afe759a4a8ff2fccb5295270a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2019
ms.locfileid: "71823538"
---
# <a name="manage-python-and-r-workloads-with-resource-governor-in-sql-server-machine-learning-services"></a>使用 SQL Server Machine Learning 服務中的 Resource Governor 管理 Python 和 R 工作負載
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

瞭解如何使用[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)來管理 SQL Server Machine Learning 服務中適用于 Python 和 R 工作負載的 CPU、實體 IO 和記憶體資源配置。

Python 和 R 中的機器學習演算法通常需要大量計算。 視您的工作負載優先順序而定，您可能需要增加或減少 Machine Learning 服務可用的資源。

如需更多一般資訊，請參閱[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)。

> [!NOTE] 
> Resource Governor 是企業版的功能。

## <a name="default-allocations"></a>預設配置

根據預設，機器學習服務的外部腳本執行時間限制為不超過全部電腦記憶體的 20%。 這取決於您的系統, 但在一般情況下, 您可能會發現此限制不足以進行重要的機器學習工作, 例如訓練模型或預測多個資料列。 

## <a name="manage-resources-with-resource-governor"></a>使用 Resource Governor 管理資源
 
根據預設，外部進程最多會在本機伺服器上使用 20% 的總主機記憶體。 您可以修改預設資源集區來進行伺服器範圍的變更, 其中 R 和 Python 進程會利用您提供給外部進程的任何容量。

或者，您可以使用相關聯的工作負載群組和分類器來建立自訂**外部資源**集區，以判斷源自特定程式、主機或您提供的其他準則之要求的資源配置。 外部資源集區是中[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]引進的一種資源集區, 可協助管理資料庫引擎外部的 R 和 Python 進程。

1. [啟用資源管理](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor)(預設為關閉)。

2. 執行 [[建立外部資源集](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql)區] 以建立並設定資源集區, 然後按[ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql)來加以執行。

3. 建立工作負載群組以進行細微的配置, 例如在定型和評分之間。

4. 建立分類器來攔截外部處理的呼叫。

5. 使用您建立的物件來執行查詢和程式。

如需逐步解說, 請參閱[如何建立外部 R 和 Python 腳本的資源集](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)區, 以取得逐步指示。

如需術語和一般概念的簡介, 請參閱[Resource Governor 資源集](../../relational-databases/resource-governor/resource-governor-resource-pool.md)區。

## <a name="processes-under-resource-governance"></a>資源治理下的進程
  
 您可以使用*外部資源集*區來管理資料庫引擎實例上下列可執行檔所使用的資源:

+ 從 SQL Server 在本機呼叫, 或使用 SQL Server 做為遠端計算內容從遠端呼叫的 Rterm
+ 從 SQL Server 本機呼叫的 Python .exe, 或使用 SQL Server 做為遠端計算內容的遠端呼叫
+ BxlServer.exe 和附屬程序
+ 啟動列的附屬進程, 例如 PythonLauncher
  
> [!NOTE]
> 不支援使用 Resource Governor 直接管理啟動控制板服務。 啟動列是受信任的服務, 只能裝載 Microsoft 所提供的啟動器。 已明確設定信任的啟動器, 以避免耗用過多的資源。
  
## <a name="next-steps"></a>後續步驟

+ [建立機器學習的資源集區](create-external-resource-pool.md)
+ [Resource Governor 資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
