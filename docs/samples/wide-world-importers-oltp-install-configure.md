---
title: 安裝和設定 WideWorldImporters 範例資料庫
description: 遵循這些指示，下載、安裝及設定具有 SQL Server Management Studio 的 WideWorldImporters 範例資料庫。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 14570059925fa5f8d8d24502c18593a118d84e37
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112440"
---
# <a name="installation-and-configuration"></a>安裝和設定
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Wide World 匯入 OLTP 資料庫安裝和設定指示。

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) （或更新版本）或[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 如需完整版本的範例，請使用 SQL Server Evaluation/Developer/Enterprise Edition。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 若要獲得最佳結果，請使用2016年6月版本或更新版本。

## <a name="download"></a>下載

範例的最新版本：

[全企業-匯入工具-發行](https://go.microsoft.com/fwlink/?LinkID=800630)

下載範例 WideWorldImporters 資料庫備份/bacpac，其對應至您的 SQL Server 或 Azure SQL Database 版本。

若要重新建立範例資料庫，您可以從下列位置取得原始程式碼。 請注意，重新建立範例會導致資料稍微不同，因為資料產生中有隨機的因素：

[全企業-匯入工具](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>安裝


### <a name="sql-server"></a>SQL Server

若要將備份還原到 SQL Server 實例，您可以使用 Management Studio。

1. 開啟 SQL Server Management Studio，並連接到目標 SQL Server 實例。
2. 以滑鼠右鍵按一下 [**資料庫**] 節點，然後選取 [**還原資料庫**]。
3. 選取 [**裝置**]，然後按一下 **[...] 按鈕。**
4. 在對話方塊中，**選取 [備份裝置**]，按一下 [**新增**]，流覽至伺服器檔案系統中的資料庫備份，然後選取備份。 按一下 [確定]  。
5. 如有需要，請在 [檔案] 窗格中變更**資料檔案和**記錄檔的目標位置。 請注意，最佳做法是將資料和記錄檔放在不同的磁片磁碟機上。
6. 按一下 [確定]  。 這會起始資料庫還原。 完成之後，您的 SQL Server 實例上會安裝資料庫 WideWorldImporters。

### <a name="azure-sql-database"></a>Azure SQL Database

若要將 bacpac 匯入新的 SQL Database，您可以使用 Management Studio。

1. 選擇性如果您在 Azure 中還沒有 SQL Server，請流覽至 [ [Azure 入口網站](https://portal.azure.com/)]，然後建立新的 SQL Database。 在建立資料庫的過程中，您將會建立伺服器。 請記下伺服器。
   - 請參閱[此教學](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)課程，以在短短幾分鐘內建立資料庫
2. 開啟 SQL Server Management Studio 並聯機到您在 Azure 中的伺服器。
3. 以滑鼠右鍵按一下 [**資料庫**] 節點，然後選取 [匯**入資料層應用程式**]。
4. 在 [匯**入設定**] 中，選取 [**從本機磁片匯入**]，然後從您的檔案系統中選取範例資料庫的 bacpac。
5. 在 [**資料庫設定**] 底下，將資料庫名稱變更為*WideWorldImporters* ，然後選取要使用的目標版本和服務目標。
6. 按 **[下一步**]，然後按一下 **[完成]** 開始進行部署。 在 P1 上完成需要幾分鐘的時間。 如果需要較低的定價層，建議您將匯入至新的 P1 資料庫，然後將定價層變更為所需的層級。

## <a name="configuration"></a>組態

### <a name="full-text-indexing"></a>全文檢索索引

範例資料庫可以利用全文檢索索引。 不過，預設不會隨 SQL Server 安裝該功能，您必須在 SQL Server 安裝期間選取它（在 Azure SQL DB 中預設為啟用）。 因此，需要進行後續安裝步驟。

1. 在 SQL Server Management Studio 中，連接到 WideWorldImporters 資料庫，然後開啟新的查詢視窗。
2. 執行下列 T-sql 命令，以啟用在資料庫中使用全文檢索索引：`EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

適用於：SQL Server

在 SQL Server 中啟用審核需要伺服器設定。 若要啟用 WideWorldImporters 範例的 SQL Server audit，請在資料庫中執行下列語句：

    EXECUTE [Application].[Configuration_ApplyAuditing]

在 Azure SQL Database 中，會透過[Azure 入口網站](https://portal.azure.com/)設定 Audit。

### <a name="row-level-security"></a>資料列層級安全性

適用于： Azure SQL Database

在 WideWorldImporters 的 bacpac 下載中，預設不會啟用資料列層級安全性。 若要在資料庫中啟用資料列層級安全性，請執行下列預存程式：

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

