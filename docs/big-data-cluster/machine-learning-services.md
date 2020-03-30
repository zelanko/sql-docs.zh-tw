---
title: 機器學習服務 (Python、R)
titleSuffix: SQL Server Big Data Clusters
description: 了解如何對安裝有機器學習服務的 SQL Server 巨量資料叢集主要執行個體，執行 Python 與 R 指令碼。
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
ms.openlocfilehash: e16304765e5f4a51feed4d3d59e790505baa740d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252028"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>對安裝有機器學習服務的 SQL Server 巨量資料叢集執行 Python 與 R 指令碼

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

您可以對安裝有[機器學習服務](../advanced-analytics/index.yml)的 [SQL Server 巨量資料叢集](big-data-cluster-overview.md)主要執行個體，執行 Python 與 R 指令碼。

> [!NOTE]
> 您也可以對 [SQL Server 語言延伸模組](../language-extensions/language-extensions-overview.md)的主要執行個體，執行 JAVA 程式碼。 執行下列步驟也能啟用語言延伸模組。

## <a name="enable-machine-learning-services"></a>啟用機器學習服務

根據預設，機器學習服務會安裝在巨量資料叢集上，而且不需要個別安裝。

若要啟用機器學習服務，請對主要執行個體上執行下列陳述式：

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

## <a name="enable-always-on-availability-groups"></a>啟用 Always On 可用性群組

若是使用 SQL Server 巨量資料叢集搭配 [Always On 可用性群組](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)，必須執行一些額外的步驟，才能啟用機器學習服務。

1. 連線到主要執行個體，再執行下列陳述式：

    ```sql
    SELECT @@SERVERNAME
    ```

    記下伺服器名稱。 在此範例中，主要執行個體的伺服器名稱為 **master-2**。

1. 對巨量資料叢集的每一個 Always On 可用性群組複本執行這些 `kubectl` 命令：

    ```
    kubectl -n bdc expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer

    kubectl -n bdc expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer

    kubectl -n bdc expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer
    ```

    您應該會看到類似如下的輸出：
    
    ```
    service/mymaster-0 exposed

    service/mymaster-1 exposed

    service/mymaster-2 exposed
    ```

1. 連線到每個主要複本端點，以便指令碼執行。

    執行下列陳述式：

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

您現在已可對巨量資料叢集的主要執行個體執行 Python 與 R 指令碼。 您可以參閱下列快速入門來執行您的第一個指令碼。

## <a name="next-steps"></a>後續步驟

+ [快速入門：使用 SQL Server 機器學習服務，建立及執行簡單的 Python 指令碼](../advanced-analytics/tutorials/quickstart-python-create-script.md)
+ [快速入門：使用 SQL Server 機器學習服務在 Python 中建立預測模型並計算其分數](../advanced-analytics/tutorials/quickstart-python-train-score-model.md)
+ [快速入門：使用 SQL Server 機器學習服務建立及執行簡單的 R 指令碼](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [快速入門：使用 SQL Server 機器學習服務在 R 中建立預測模型並計算其分數](../advanced-analytics/tutorials/quickstart-r-train-score-model.md)
