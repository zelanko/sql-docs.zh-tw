---
title: 安裝及設定 WideWorldImporters 範例資料庫-SQL |Microsoft Docs
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
ms.openlocfilehash: c31c6c2071d276da9b3ab0e498a090659ba589a7
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51673477"
---
# <a name="installation-and-configuration"></a>安裝和組態
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Wide World Importers OLTP 資料庫安裝和組態指示。

## <a name="prerequisites"></a>先決條件

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) （或更新版本） 或[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 此範例的完整版本，使用 SQL Server Evaluation/開發人員/Enterprise Edition。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 對於獲得最佳結果，請使用 2016 年 6 月版本或更新版本。

## <a name="download"></a>下載

最新版的範例：

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

將範例 WideWorldImporters 資料庫備份/bacpac 下載對應至您的 SQL Server 或 Azure SQL Database 的版本。

若要重新建立範例資料庫的原始程式碼可從下列位置。 請注意，重新建立此範例會導致有些微的差異資料，因為在資料產生隨機的因素：

[wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>安裝


### <a name="sql-server"></a>[SQL Server]

若要將備份還原到 SQL Server 執行個體，您可以使用 Management Studio。

1. 開啟 SQL Server Management Studio 並連接至目標 SQL Server 執行個體。
2. 以滑鼠右鍵按一下**資料庫**節點，然後選取**Restore Database**。
3. 選取 **裝置**，然後按一下按鈕 **...**
4. 在對話方塊**選取備份裝置**，按一下**新增**，瀏覽至伺服器的檔案系統中的資料庫備份，並選取備份。 按一下 [確定] 。
5. 如有需要變更資料的目標位置，並在記錄檔**檔案**窗格。 請注意，您要放置資料和記錄檔在不同的磁碟機上的最佳作法。
6. 按一下 [確定] 。 這會起始資料庫還原。 完成之後，您必須安裝在您的 SQL Server 執行個體上的 WideWorldImporters 的資料庫。

### <a name="azure-sql-database"></a>Azure SQL Database

若要將 bacpac 匯入新的 SQL Database 中，您可以使用 Management Studio。

1. （選擇性）如果您還沒有 SQL Server 在 Azure 中，瀏覽至[Azure 入口網站](https://portal.azure.com/)並建立新的 SQL Database。 在進行的建立資料庫，您將建立伺服器。 請記下的伺服器。
   - 請參閱[本教學課程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)分鐘內建立資料庫
2. 開啟 SQL Server Management Studio 並連接到您在 Azure 中的伺服器。
3. 以滑鼠右鍵按一下**資料庫**節點，然後選取**匯入資料層應用程式**。
4. 在 **匯入設定**選取**從本機磁碟匯入**和選取範例資料庫的 bacpac 從檔案系統。
5. 底下**資料庫設定**變更的資料庫名稱*WideWorldImporters*和選取要使用的目標版本和服務目標。
6. 按一下 **下一步**並**完成**開始進行部署。 它會在 P1 上完成幾分鐘的時間。 如果較低的定價層是所需，建議您將新的 P1 資料庫，匯入，然後將定價層變更為所需的層級。

## <a name="configuration"></a>組態

### <a name="full-text-indexing"></a>全文檢索索引

範例資料庫可使用的全文檢索索引。 不過，該功能不會安裝 SQL server 的預設值-您必須選取期間 （已啟用預設會在 Azure SQL DB） 的 SQL Server 安裝程式。 因此，就需要後續安裝步驟。

1. 在 SQL Server Management Studio 中，連接到 WideWorldImporters 資料庫並開啟新的查詢視窗。
2. 執行下列 T-SQL 命令來啟用資料庫中的全文檢索索引：  `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

適用於： SQL Server

啟用 SQL Server 中的稽核需要伺服器的設定。 若要啟用 SQL Server 稽核，WideWorldImporters 範例，請在資料庫中執行下列陳述式：

    EXECUTE [Application].[Configuration_ApplyAuditing]

透過 Azure SQL database 設定稽核[Azure 入口網站](https://portal.azure.com/)。

### <a name="row-level-security"></a>資料列層級安全性

適用於： Azure SQL Database

根據預設，WideWorldImporters bacpac 下載在未啟用資料列層級安全性。 若要啟用資料庫中的資料列層級安全性，請執行下列預存程序：

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

