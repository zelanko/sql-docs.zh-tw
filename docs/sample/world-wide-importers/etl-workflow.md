---
title: "ETL 工作流程 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology: samples
ms.custom: 
ms.date: 06/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 679e58fe-b062-4934-a94c-9bb916b0bcb0
caps.latest.revision: "5"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: bbda77b86b4c804ae0cf261f54f51fc487090e1d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 工作流程
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]ETL 封裝 WWI_Integration 用來將資料從 WideWorldImporters 資料庫移轉到 WideWorldImportersDW 資料庫，當資料變更。 封裝會定期執行 （通常每日）。

## <a name="overview"></a>概觀

設計的封裝會使用 SQL Server Integration Services (SSIS) 來協調大量 T-SQL 作業 （而不是當做個別轉換 SSIS 中） 以確保高效能。

維度會載入第一次，然後再按照事實資料表。 在失敗後的任何時間，可以重新執行封裝。

工作流程如下所示：

 ![WideWorldImporters ETL 工作流程](../../sample/world-wide-importers/media/wideworldimporters-etl-workflow.png)

開始運作的 「 運算式 」 工作與適當的時間點。 此時間是目前的時間較少幾分鐘的時間。 （這是要求資料的權限到目前的時間比更健全）。 然後，它會截斷任何時間 （毫秒）。

主要處理一開始會填入日期維度資料表。 它會確保資料表中，已填入目前年度的所有日期。

在此之後，一系列的資料流程工作會載入每個維度，則每一個事實。

## <a name="prerequisites"></a>必要條件

- SQL Server 2016 （或更新版本） 與 WideWorldImporters 和 WideWorldImportersDW 資料庫。 這些可以在相同或不同 SQL Server 執行個體上。
- SQL Server Management Studio (SSMS)
- SQL Server 2016 Integration Services (SSIS)。
  - 請確定您已建立 SSIS 目錄。 如果沒有，請以滑鼠右鍵按一下**Integration Services**在 SSMS 物件總管] 中，選擇 [**加入目錄**。 遵循的預設值。 它會要求您啟用 sqlclr 及提供密碼。


## <a name="download"></a>下載

最新版的範例：

[wide world-匯入工具版本](http://go.microsoft.com/fwlink/?LinkID=800630)

SSIS 封裝檔案下載**每日 ETL.ispac**。

重新建立範例資料庫的原始程式碼可從下列位置。

[匯入 world wide 工具](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)

## <a name="install"></a>Install

1. 部署 SSIS 封裝。
   - 從 Windows 檔案總管中開啟 「 每日 ETL.ispac"封裝。 這會啟動 Integration Services 部署精靈。
   - 在 [選取來源] 之後，預設專案的部署，指向 「 每日 ETL.ispac 」 封裝的路徑。
   - 在 [選取目的地] 下輸入主控 SSIS 目錄的伺服器名稱。
   - 選取 SSIS 目錄中，例如在新的資料夾"WideWorldImporters"下的路徑。
   - 完成精靈，即可部署程序。

2. 建立 ETL 程序的 SQL Server Agent 作業。
   - 在 SSMS 中，以滑鼠右鍵按一下 「 SQL Server 代理程式 」，然後選擇 新增-> 作業。
   - 挑選的名稱，例如"WideWorldImporters ETL"。
   - 新增作業步驟的型別"SQL Server Integration Services 封裝。
   - 選取 SSIS 目錄中，伺服器並選取 「 每日 ETL"封裝。
   - 設定 下-> 連接管理員確認已正確設定通往來源和目標。 預設為連接到本機執行個體。
   - 按一下 [確定] 來建立作業。

3. 執行或排程作業。
