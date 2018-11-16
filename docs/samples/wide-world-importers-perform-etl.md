---
title: WideWorldImportersDW-ETL 工作流程 |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d17cc2ccc46733c857f884f78a1b0c9b3f980586
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674107"
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 工作流程
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
使用*WWI_Integration* ETL 封裝，以將資料從 WideWorldImporters 資料庫移轉至 WideWorldImportersDW 資料庫，隨著資料變更。 封裝會定期執行 （通常是每天）。

封裝可使用 SQL Server Integration Services 來協調大量 T-SQL 作業 （而不是 Integration Services 中的個別轉換），以確保高效能。

首先，載入的維度和事實資料表再載入。 您可以隨時在失敗後重新執行封裝。

工作流程看起來像這樣：

 ![WideWorldImporters ETL 工作流程](media/wide-world-importers/wideworldimporters-etl-workflow.png)

工作流程啟動時，決定適當的截止時間的 「 運算式 」 工作。 截止時間為目前時間減去幾分鐘的時間。 （這種方法是比要求的目前時間的資料權限更健全的）。任何毫秒會被截斷的時間。

主要處理一開始會填入日期維度資料表。 處理程序可確保資料表中，已填入所有目前的年份日期。

接下來，資料流程工作的一系列會載入每個維度。 接著，它們會載入每一個事實。

## <a name="prerequisites"></a>先決條件

- SQL Server 2016 （或更新版本），WideWorldImporters 和 WideWorldImportersDW 的資料庫 （在相同或不同 SQL Server 執行個體）
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - 請確定您建立的 Integration Services 目錄。 若要建立的 Integration Services 目錄中，在 SQL Server Management Studio 物件總管中，以滑鼠右鍵按一下**Integration Services**，然後選取**新增目錄**。 保留預設選項。 系統會提示您啟用 [SQLCLR] 並提供密碼。


## <a name="download"></a>下載

如範例的最新版本，請參閱 <<c0> [ 整個 world importers-發行](https://go.microsoft.com/fwlink/?LinkID=800630)。 下載*每日 ETL.ispac* Integration Services 封裝檔案。

如需重新建立範例資料庫的原始程式碼，請參閱[匯入 world wide 工具](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)。

## <a name="install"></a>安裝

1. 部署 Integration Services 封裝：
   1. 在 Windows 檔案總管中，開啟*每日 ETL.ispac*封裝。 這會啟動 SQL Server Integration Services 部署精靈。
   2. 底下**選取來源**，遵循專案部署的預設值，具有指向路徑*每日 ETL.ispac*封裝。
   3. 底下**選取目的地**，輸入裝載的 Integration Services 目錄的伺服器名稱。
   4. 比方說，選取名為的新資料夾中的 Integration Services 目錄下的路徑*WideWorldImporters*。
   5. 選取 **部署**以完成精靈。

2. 建立 SQL Server Agent 作業的 ETL 程序：
   1. 在 Management Studio 中，以滑鼠右鍵按一下**SQL Server Agent**，然後選取**新增** > **作業**。
   2. 例如，輸入名稱， *WideWorldImporters ETL*。
   3. 新增**作業步驟**型別的**SQL Server Integration Services 封裝**。
   4. 選取已在 Integration Services 類別目錄的伺服器，然後選取*每日 ETL*封裝。
   5. 底下**組態** > **連接管理員**，確保已正確設定來源和目標的連線。 預設為連接到本機執行個體。
   6. 選取 **確定**來建立作業。

3. 執行或排程作業。
