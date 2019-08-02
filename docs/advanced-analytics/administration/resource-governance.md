---
title: R 和 Python 腳本執行的資源管理
description: 為 SQL Server 資料庫引擎實例上的 R 和 Python 工作負載配置 RAM 記憶體、CPU 和 IO。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 55a83e7e63a4e43afe1168aab3307f2806a55fca
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715267"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>SQL Server 中機器學習服務的資源管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

資料科學和機器學習演算法需要大量計算。 視工作負載優先順序而定, 您可能需要增加資料科學可用的資源, 或如果 R 和 Python 腳本執行破壞其他同時執行的服務效能, 則降低資源。 

當您需要重新平衡多個工作負載之間的系統資源配置時, 可以使用[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)來配置 R 和 Python 的外部執行時間所使用的 CPU、實體 IO 和記憶體資源。 如果您轉移資源配置, 請記住, 您可能也需要減少針對其他工作負載和服務所保留的記憶體數量。 

> [!NOTE] 
> Resource Governor 是企業版的功能。

## <a name="default-allocations"></a>預設配置

根據預設, 機器學習服務的外部腳本執行時間限制為不超過全部電腦記憶體的 20%。 這取決於您的系統, 但在一般情況下, 您可能會發現此限制不足以進行重要的機器學習工作, 例如訓練模型或預測多個資料列。 

## <a name="use-resource-governor-to-control-resourcing"></a>使用 Resource Governor 來控制管理
 
根據預設, 外部進程最多會在本機伺服器上使用 20% 的總主機記憶體。 您可以修改預設資源集區來進行伺服器範圍的變更, 其中 R 和 Python 進程會利用您提供給外部進程的任何容量。

或者, 您可以使用相關聯的工作負載群組和分類器來建立自訂*外部資源*集區, 以判斷源自特定程式、主機或您提供的其他準則之要求的資源配置。 外部資源集區是中[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]引進的一種資源集區, 可協助管理資料庫引擎外部的 R 和 Python 進程。

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
  
## <a name="see-also"></a>另請參閱

+ [管理機器學習整合](../r/managing-and-monitoring-r-solutions.md)
+ [建立機器學習的資源集區](../r/how-to-create-a-resource-pool-for-r.md)
+ [Resource Governor 資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
