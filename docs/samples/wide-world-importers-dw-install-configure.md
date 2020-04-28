---
title: 安裝 & 設定 DW WideWorldImporters 範例資料庫
description: 遵循這些指示，下載、安裝及設定具有 SQL Server Management Studio 的 WideWorldImportersDW 範例資料庫。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 2f640415ecdc2ae4a48220aeec2a2c78ed79807c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488541"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW 安裝和設定
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW 資料庫的安裝和設定指示。

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) （或更新版本）或[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 若要使用完整版的範例，請使用 SQL Server Evaluation/Developer/Enterprise Edition。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 若要獲得最佳結果，請使用2016年6月版本或更新版本。

## <a name="download"></a>下載

範例的最新版本：

[全企業-匯入工具-發行](https://go.microsoft.com/fwlink/?LinkID=800630)

下載範例 WideWorldImportersDW 資料庫備份/bacpac，其對應至您的 SQL Server 或 Azure SQL Database 版本。

若要重新建立範例資料庫，您可以從下列位置取得原始程式碼。 請注意，資料填入是以 OLTP 資料庫（WideWorldImporters）中的 ETL 為基礎：

[全世界-匯入工具-來源](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

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
5. 在 [**資料庫設定**] 底下，將資料庫名稱變更為*WideWorldImportersDW* ，然後選取要使用的目標版本和服務目標。
6. 按 **[下一步**]，然後按一下 **[完成]** 開始進行部署。 這需要幾分鐘才能完成。 指定低於 S2 的服務目標時，可能需要較長的時間。

## <a name="configuration"></a>設定

[適用于 SQL Server 2016 （和更新版本）開發人員/評估版/Enterprise Edition]

範例資料庫可利用 PolyBase 來查詢 Hadoop 或 Azure blob 儲存體中的檔案。 不過，預設不會隨 SQL Server 安裝該功能，您必須在 SQL Server 安裝期間加以選取。 因此，需要進行後續安裝步驟。

1. 在 SQL Server Management Studio 中，連接到 WideWorldImportersDW 資料庫，然後開啟新的查詢視窗。
2. 執行下列 T-sql 命令，以啟用資料庫中的 PolyBase 使用方式：

   執行 [應用程式]。[Configuration_ApplyPolyBase]
