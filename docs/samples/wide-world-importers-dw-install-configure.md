---
title: WideWorldImporters OLAP 範例資料庫-安裝和設定-SQL |Microsoft 文件
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
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 79df863a46adfd9bbdfd2a24b12a79592fdab6bd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW 安裝和設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
WideWorldImportersDW 資料庫的安裝和組態指示。

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) （或更新版本） 或[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 若要使用此範例的完整版本，請使用 SQL Server Evaluation/Developer/Enterprise Edition。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 對於獲得最佳結果，請使用 2016 年 6 月版本或更新版本。

## <a name="download"></a>下載

最新版的範例：

[wide-world-importers-release](http://go.microsoft.com/fwlink/?LinkID=800630)

將範例 WideWorldImportersDW 資料庫備份/bacpac 下載對應至 SQL Server 或 Azure SQL Database 的版本。

重新建立範例資料庫的原始程式碼可從下列位置。 請注意，資料母體擴展基礎 ETL OLTP 資料庫 (WideWorldImporters):

[wide-world-importers-source](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>安裝


### <a name="sql-server"></a>SQL Server

若要將備份還原到 SQL Server 執行個體，您可以使用 Management Studio。

1. 開啟 SQL Server Management Studio 並連接到目標 SQL Server 執行個體。
2. 以滑鼠右鍵按一下**資料庫**節點，然後選取**Restore Database**。
3. 選取**裝置**和按一下按鈕 **...**
4. 在對話方塊中**選取備份裝置**，按一下 **新增**、 瀏覽至伺服器的檔案系統中的資料庫備份，以及選取的備份。 按一下 **[確定]**。
5. 視需要變更資料的目標位置，然後在記錄檔，**檔案**窗格。 請注意，則最佳做法是將資料和記錄檔，在不同的磁碟機上。
6. 按一下 **[確定]**。 這會起始資料庫還原。 完成之後，您必須安裝在您的 SQL Server 執行個體上的 WideWorldImporters 的資料庫。

### <a name="azure-sql-database"></a>Azure SQL Database

若要將 bacpac 匯入新的 SQL 資料庫，您可以使用 Management Studio。

1. （選擇性）如果您還沒有 SQL Server 在 Azure 中，瀏覽至[Azure 入口網站](https://portal.azure.com/)並建立新的 SQL 資料庫。 在進行的建立資料庫，您將建立的伺服器。 請記下的伺服器。
   - 請參閱[本教學課程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)建立資料庫，以分鐘為單位
2. 開啟 SQL Server Management Studio 並連接到 Azure 中的伺服器。
3. 以滑鼠右鍵按一下**資料庫**節點，然後選取**匯入資料層應用程式**。
4. 在**匯入設定**選取**從本機磁碟匯入**和選取範例資料庫的 bacpac 從檔案系統。
5. 在下**資料庫設定**變更資料庫名稱以*WideWorldImportersDW*和選取要使用的目標版本和服務目標。
6. 按一下**下一步**和**完成**開始進行部署。 它會需要幾分鐘才能完成。 指定服務目標比 S2 低時可能需要較長。

## <a name="configuration"></a>組態

[適用於 SQL Server 2016 （含） 以後開發人員/Evaluation Enterprise Edition]

範例資料庫可以利用 PolyBase Hadoop 或 Azure blob 儲存體中的查詢檔案。 不過，根據預設，使用 SQL Server 未安裝該功能-您需要在 SQL Server 安裝程式期間選取。 因此，就需要後續安裝步驟。

1. 在 SQL Server Management Studio，連接到 WideWorldImportersDW 資料庫並開啟新的查詢視窗。
2. 執行下列 T-SQL 命令來啟用資料庫中的 PolyBase:

   執行 [應用程式]。[Configuration_ApplyPolyBase]
