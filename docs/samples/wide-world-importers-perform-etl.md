---
title: 廣域國際進口商DW - ETL工作流程 |微軟文件
description: 將 ETL 包與 SQL 伺服器整合服務 (SSIS) 一起定期將數據從廣域世界導入者資料庫遷移到廣域世界導入者DW。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 98ce2b9aa11b2e1381da1f16455df8a2c0d3f243
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487427"
---
# <a name="wideworldimportersdw-etl-workflow"></a>廣域國際進口商DW ETL工作流程
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
使用*WWI_Integration* ETL 包將數據從寬世界進口商資料庫遷移到 WideWorld 導入者DW 資料庫,因為數據發生更改。 包定期運行(通常每天)。

該包通過使用 SQL Server 整合服務來協調批量 T-SQL 操作(而不是在整合服務中進行單獨的轉換),從而確保高性能。

首先載入維度,然後載入事實表。 在發生故障後,您可以隨時重新運行包。

工作流如下所示:

 ![廣域國際進口商 ETL 工作流程](media/wide-world-importers/wideworldimporters-etl-workflow.png)

工作流從確定適當截止時間的表達式任務開始。 截止時間是當前時間減去幾分鐘。 (此方法比直接請求數據到當前時間更可靠。任何毫秒都從時間被截斷。

主處理首先填充日期維度表。 處理可確保在表中填充了當前年份的所有日期。

接下來,一系列數據流任務載入每個維度。 然後,它們載入每個事實。

## <a name="prerequisites"></a>Prerequisites

- SQL Server 2016(或更高版本),具有寬世界導入器和廣域國際導入器DW資料庫(在 SQL 伺服器的相同或不同情況下)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - 確保創建整合服務目錄。 要建立整合式服務目錄,請在 SQL 伺服器管理工作室物件資源管理器中,右鍵單擊**整合服務**,然後選擇「**添加目錄**」。 保留默認選項。 系統將提示您啟用 SQLCLR 並提供密碼。


## <a name="download"></a>下載

有關該範例的最新版本,請參閱[全球進口商版本](https://go.microsoft.com/fwlink/?LinkID=800630)。 下載*每日 ETL.ispac*整合服務包檔。

有關重新建立範例資料庫的源碼,請參閱[全球匯入者](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-ssis)。

## <a name="install"></a>安裝

1. 部署整合服務套件:
   1. 在 Windows 資源管理器中,打開*每日 ETL.ispac*包。 這將啟動 SQL 伺服器整合服務部署精靈。
   2. 在**選擇源**下,按照專案部署的預設值操作,路徑指向每日*ETL.ispac*包。
   3. 在**選擇目標**「下,輸入承載整合服務目錄的伺服器的名稱。
   4. 在整合服務目錄下選擇路徑,例如,在名為*WideWorld 導入器*的新資料夾中選擇路徑。
   5. 選擇 **「部署」** 以完成精靈。

2. 為 ETL 程序建立 SQL 伺服器代理作業:
   1. 在管理工作室中,右鍵單擊**SQL 伺服器代理**,然後選擇 **「新** > **作業**」。
   2. 輸入名稱,例如,*寬世界進口商 ETL*。
   3. 新增**SQL 伺服器整合服務套件**型態的**工作步驟**。
   4. 選擇具有整合服務目錄的伺服器,然後選擇*每日 ETL*包。
   5. 在**配置** > **連接管理員**下,確保正確配置到源和目標的連接。 預設值是連接到本地實例。
   6. 選擇 **「確定」** 以建立作業。

3. 執行或安排作業。
