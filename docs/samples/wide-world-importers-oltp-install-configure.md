---
title: 安裝並設定廣域進口者範例資料庫
description: 按照這些說明使用 SQL Server 管理工作室下載、安裝和配置 WideWorld 導入器範例資料庫。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 355eaa254fcc7bb6cd4aa9a39c2cbcb269d88396
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487067"
---
# <a name="installation-and-configuration"></a>安裝和組態
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
全球進口商 OLTP 資料庫安裝和配置說明。

## <a name="prerequisites"></a>Prerequisites

- [SQL 伺服器 2016(](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)或更高)或[Azure SQL 資料庫](https://azure.microsoft.com/services/sql-database/)。 對於範例的完整版本,請使用 SQL 伺服器評估/開發人員/企業版。
- [SQL 伺服器管理工作室](../ssms/download-sql-server-management-studio-ssms.md)。 為獲得最佳效果,請使用 2016 年 6 月版本或更高版本。

## <a name="download"></a>下載

範例的最新版本:

[全球進口商發佈](https://go.microsoft.com/fwlink/?LinkID=800630)

下載與 SQL Server 或 Azure SQL 資料庫版本對應的範例 WideWorld 匯入者資料庫備份/bacpac。

要重新建立範例資料庫的原始程式碼可從以下位置獲得。 請注意,重新建立範例將導致資料略有不同,因為資料生成中有一個隨機因素:

[廣泛的世界進口商](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

## <a name="install"></a>安裝


### <a name="sql-server"></a>SQL Server

要將備份還原到 SQL Server 實例,可以使用管理工作室。

1. 打開 SQL 伺服器管理工作室並連接到目標 SQL Server 實例。
2. 右鍵單擊**資料庫**節點,然後選擇 **「還原資料庫**」。。
3. 選擇**裝置**並按下按鈕 **...**
4. 在對話框中選擇**備份設備**,按一下「**添加**」,導航到伺服器檔系統中的資料庫備份,然後選擇備份。 按一下 [確定]  。
5. 如果需要,請更改「**檔」** 窗格中資料和紀錄檔的目標位置。 請注意,最佳做法是將數據和日誌檔放在不同的驅動器上。
6. 按一下 [確定]  。 這將啟動資料庫還原。 完成後,您將在 SQL Server 實例上安裝資料庫 WideWorld 導入器。

### <a name="azure-sql-database"></a>Azure SQL Database

要將百家樂導入新的 SQL 資料庫,可以使用管理工作室。

1. ( 選擇性的 )如果 Azure 中尚未有 SQL 伺服器,請導航到[Azure 門戶](https://portal.azure.com/)並創建新的 SQL 資料庫。 在建立資料庫的過程中,您將創建一個伺服器。 記下伺服器。
   - 請參閱[本教程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/),在幾分鐘內創建数据庫
2. 打開 SQL 伺服器管理工作室並連接到 Azure 中的伺服器。
3. 右鍵按下**資料庫**節點,然後選擇**匯入資料層應用程式**。
4. 在「**導入設定」** 中選擇 **「從本地磁碟匯入**」,然後從檔案系統中選擇範例資料庫的百科。
5. 在 **「資料庫設定」** 下,將資料庫名稱更改為*WideWorld 導入器*,並選擇要使用的目標版本和服務目標。
6. 按下「**下一步**」 並**完成**以啟動部署。 在 P1 上完成需要幾分鐘時間。 如果需要較低的定價層,建議將其導入到新的 P1 資料庫中,然後將定價層更改為所需的級別。

## <a name="configuration"></a>組態

### <a name="full-text-indexing"></a>全文檢索索引

示例資料庫可以使用全文索引。 但是,默認情況下,該功能不會與 SQL Server 一起安裝 - 您需要在 SQL Server 設定期間選擇它(預設情況下在 Azure SQL DB 中啟用此功能)。 因此,需要安裝後步驟。

1. 在 SQL 伺服器管理工作室中,連接到寬世界導入器資料庫並打開新的查詢視窗。
2. 執行以下 T-SQL 指令,以便在資料庫中使用全文索引:`EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

適用於：SQL Server

在 SQL Server 中啟用審核需要伺服器配置。 要為 WideWorld 匯入器範例啟用 SQL Server 稽核,在資料庫中執行以下語句:

    EXECUTE [Application].[Configuration_ApplyAuditing]

在 Azure SQL 資料庫中,審核通過[Azure 門戶](https://portal.azure.com/)進行配置。

### <a name="row-level-security"></a>資料列層級安全性

套用於:Azure SQL 資料庫

默認情況下,在寬世界進口商的 bacpac 下載中,不會啟用行級安全性。 要在資料庫中啟用列級安全性,請執行以下儲存過程:

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

