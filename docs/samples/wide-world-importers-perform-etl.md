---
title: WideWorldImportersDW-ETL 工作流程 |Microsoft Docs
description: 使用 ETL 套件搭配 SQL Server Integration Services （SSIS），定期將資料從 WideWorldImporters 資料庫移轉至 WideWorldImportersDW。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 000d12b97eb2eefbfcd9a6a73e02c0098b2afdbb
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112393"
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 工作流程
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
當資料變更時，請使用*WWI_Integration* ETL 封裝，將資料從 WideWorldImporters 資料庫移轉到 WideWorldImportersDW 資料庫。 封裝會定期執行（通常是每天）。

封裝會使用 SQL Server Integration Services 來協調大量 T-sql 作業（而不是 Integration Services 中的個別轉換），以確保高效能。

首先會載入維度，然後載入事實資料表。 您可以在失敗之後隨時重新執行封裝。

工作流程看起來像這樣：

 ![WideWorldImporters ETL 工作流程](media/wide-world-importers/wideworldimporters-etl-workflow.png)

工作流程的開頭是運算式工作，可決定適當的截止時間。 截止時間是目前時間減去數分鐘。 （這種方法比目前時間要求的資料更穩固）。任何毫秒都會從時間截斷。

主要處理是從填入「日期」維度資料表開始。 此處理可確保已在資料表中填入目前年份的所有日期。

接下來，一系列的資料流程工作會載入每個維度。 然後，他們會載入每個事實。

## <a name="prerequisites"></a>Prerequisites

- SQL Server 2016 （或更新版本），其中包含 WideWorldImporters 和 WideWorldImportersDW 資料庫（在相同或不同的 SQL Server 實例中）
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - 請確定您建立的是 Integration Services 目錄。 若要建立 Integration Services 目錄，請在 SQL Server Management Studio 物件總管中，以滑鼠右鍵按一下 [ **Integration Services**]，然後選取 [**新增目錄**]。 保留預設選項。 系統會提示您啟用 SQLCLR 並提供密碼。


## <a name="download"></a>下載

如需最新版本的範例，請參閱 wide-匯[入工具-發行](https://go.microsoft.com/fwlink/?LinkID=800630)。 下載*每日 .ispac* Integration Services 封裝檔案。

若要讓原始程式碼重新建立範例資料庫，請參閱[wide world-匯入](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)工具。

## <a name="install"></a>安裝

1. 部署 Integration Services 套件：
   1. 在 Windows Explorer 中，開啟*每日的 .ispac*套件。 這會啟動 SQL Server Integration Services 部署嚮導。
   2. 在 [**選取來源**] 底下，遵循專案部署的預設值，並將路徑指向 [*每日 .ispac* ] 套件。
   3. 在 [**選取目的地**] 底下，輸入裝載 Integration Services 目錄的伺服器名稱。
   4. 在 [Integration Services 目錄] 底下選取路徑，例如，在名為*WideWorldImporters*的新資料夾中。
   5. 選取 [**部署**] 以完成嚮導。

2. 建立 ETL 進程的 SQL Server Agent 作業：
   1. 在 Management Studio 中，以滑鼠右鍵按一下 [ **SQL Server Agent**]，然後選取 [**新增** > **作業**]。
   2. 輸入名稱，例如*WIDEWORLDIMPORTERS ETL*。
   3. 新增**SQL Server Integration Services 封裝**類型的**作業步驟**。
   4. 選取具有 [Integration Services 目錄] 的伺服器，然後選取 [*每日 ETL* ] 套件。
   5. 在 [設定**連線管理員**] 下，確定已正確設定與來源和目標的連接。 **Configuration**  >  預設值是連接到本機實例。
   6. 選取 **[確定]** 以建立作業。

3. 執行或排程工作。
