---
title: R 和 Python 指令碼執行-SQL Server 機器學習的資源管理
description: SQL Server database engine 執行個體上的 R 和 Python 工作負載配置 RAM 記憶體、 CPU 和 IO。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2e8b3122f4083d419797abeef5ff96944bac3e6a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512985"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>SQL Server 中的機器學習的資源控管
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

資料科學和機器學習演算法會耗用大量運算資源。 根據工作負載優先順序，您可能需要增加用於資料科學的資源，或減少資源如果 R 和 Python 指令碼執行會逐漸破壞同時執行的其他服務的效能。 

當您需要跨多個工作負載平衡系統資源的分佈時，您可以使用[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)配置 CPU、 實體 IO 和記憶體資源的外部執行階段使用 R 和 Python。 如果您轉移資源配置，請記住，您可能需要也減少保留給其他工作負載和服務的記憶體數量。 

> [!NOTE] 
> 資源管理員是 Enterprise Edition 的功能。

## <a name="default-allocations"></a>預設配置

根據預設，適用於 machine learning 的外部指令碼執行階段僅限於不超過 20%的總機器記憶體。 這取決於您的系統，但在一般情況下，您可能會發現這項限制不足嚴重的機器學習工作，例如定型模型或預測多個資料列上。 

## <a name="use-resource-governor-to-control-resourcing"></a>若要控制資源使用資源管理員
 
根據預設，外部處理序會使用最多 20%的主機記憶體總計，在本機伺服器上。 您可以修改預設資源集區，以進行伺服器端的變更，使用 R 和 Python 處理程序利用任何容量您提供給外部處理序。

或者，您可以建構自訂*外部資源集區*、 相關聯的工作負載群組和分類器，以判斷源自於特定的程式、 主機或其他準則的要求的資源配置，您提供。 外部資源集區是一種資源集區中導入[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]來協助您管理的 R 和 Python 處理程序外部的資料庫引擎。

1. [啟用資源監管](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor)（它預設為關閉）。

2. 執行[CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql)來建立和設定資源集區，後面接著[ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql)來實作它。

3. 建立細微的配置，例如之間訓練和評分的工作負載群組。

4. 建立分類器來攔截外部處理的呼叫。

5. 執行查詢和使用您所建立之物件的程序。

如需逐步解說，請參閱 <<c0> [ 如何建立外部 R 和 Python 指令碼的資源集區](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)如需逐步指示。

術語和一般概念的簡介，請參閱 < [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。

## <a name="processes-under-resource-governance"></a>資源控管下的程序
  
 您可以使用*外部資源集區*來管理資料庫引擎執行個體上的下列可執行檔所使用的資源：

+ Rterm.exe 時呼叫從 SQL Server 的本機或遠端呼叫 SQL Server 作為遠端計算內容
+ Python.exe 時呼叫從 SQL Server 的本機或遠端呼叫 SQL Server 作為遠端計算內容
+ BxlServer.exe 和附屬程序
+ 啟動的啟動列，例如 PythonLauncher.dll 的附屬處理序
  
> [!NOTE]
> 不支援直接管理 Launchpad 服務所使用資源管理員。 啟動列 是受信任的服務，可以只由 Microsoft 所提供的主應用程式啟動程式。 若要避免過度使用資源明確設定受信任的啟動器。
  
## <a name="see-also"></a>另請參閱

+ [管理 machine learning 整合](../r/managing-and-monitoring-r-solutions.md)
+ [建立機器學習的資源集區](../r/how-to-create-a-resource-pool-for-r.md)
+ [資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
