---
title: WideWorldImportersDW-ETL 工作流程 |Microsoft 文件
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 36638c4cc2bda58ac277822d5c4a4ce5421ab8b4
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467684"
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 工作流程
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
使用*WWI_Integration* ETL 封裝，將資料從 WideWorldImporters 資料庫移轉到 WideWorldImportersDW 資料庫，當資料變更時。 封裝會定期執行 （通常是每日）。

封裝可高效能確保使用 SQL Server Integration Services 來協調大量 T-SQL 作業 （而不是在 Integration Services 中的個別轉換）。

首先，載入維度和事實資料表的載入然後。 您可以隨時在失敗後重新執行封裝。

工作流程看起來像這樣：

 ![WideWorldImporters ETL 工作流程](media/wide-world-importers/wideworldimporters-etl-workflow.png)

使用 「 運算式 」 工作會決定適當的時間點開始工作流程。 時間點是目前時間減去幾分鐘的時間。 （這種方法是要求資料的權限到目前的時間比更健全的）。任何 （毫秒） 會被截斷的時間。

主要處理一開始會填入日期維度資料表。 處理可確保資料表中，已填入目前年度的所有日期。

接下來，一系列的資料流程工作載入的每個維度。 然後，它們會載入每個事實。

## <a name="prerequisites"></a>필수 구성 요소

- SQL Server 2016 （或更新版本），與 WideWorldImporters 和 WideWorldImportersDW 資料庫 （在相同或不同的執行個體的 SQL Server）
- Transact-SQL
- SQL Server 2016 Integration Services
  - 請確定您建立的 Integration Services 目錄。 若要建立的 Integration Services 目錄中，SQL Server Management Studio 物件總管 中，以滑鼠右鍵按一下**Integration Services**，然後選取**加入目錄**。 保留預設選項。 系統會提示您啟用 SQLCLR 並提供的密碼。


## <a name="download"></a>下載

如範例的最新版本，請參閱[wide world-匯入工具版本](http://go.microsoft.com/fwlink/?LinkID=800630)。 下載*每日 ETL.ispac* Integration Services 封裝檔案。

若要重新建立範例資料庫的原始程式碼，請參閱[匯入 world wide 工具](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)。

## <a name="install"></a>安裝

1. 部署 Integration Services 封裝：
   1. 在 Windows 檔案總管 中，開啟*每日 ETL.ispac*封裝。 這會啟動 SQL Server Integration Services 部署精靈。
   2. 在下**選取來源**，遵循專案部署的預設值，具有指向路徑*每日 ETL.ispac*封裝。
   3. 在下**選取目的地**，輸入主控 Integration Services 目錄的伺服器名稱。
   4. 例如，選取名為新資料夾中的下的 Integration Services 類別目錄中的路徑*WideWorldImporters*。
   5. 選取**部署**以完成精靈。

2. 建立 SQL Server Agent 作業的 ETL 程序：
   1. 在 Management Studio 中，以滑鼠右鍵按一下**SQL Server Agent**，然後選取**新增** > **作業**。
   2. 例如，輸入名稱， *WideWorldImporters ETL*。
   3. 新增**作業步驟**型別的**SQL Server Integration Services 封裝**。
   4. 選取的 Integration Services 類別目錄中的伺服器，然後選取*每日 ETL*封裝。
   5. 在下**組態** > **連接管理員**，確認已正確設定通往來源和目標。 預設為連接到本機執行個體。
   6. 選取**確定**建立作業。

3. 執行或排程作業。
