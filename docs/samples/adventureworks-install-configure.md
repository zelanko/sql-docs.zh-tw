---
title: 安裝和設定 AdventureWorks 範例資料庫-SQL |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7881400c3e4696426b1999229e917630cf905d0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657508"
---
# <a name="adventureworks-installation-and-configuration"></a>AdventureWorks 安裝和設定
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks 下載連結和安裝指示。 

## <a name="prerequisites"></a>先決條件

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)或是[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 此範例的完整版本，使用 SQL Server Evaluation/開發人員/Enterprise Edition。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 對於獲得最佳結果，請使用 2016 年 6 月版本或更新版本。
 
## <a name="github-links"></a>Github 連結

- [所有 sql 2014 2016年的 AdventureWorks 檔案](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL 2012 的所有 AdventureWorks 檔案](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [所有適用於 SQL 2008 和 2008 r2 的 AdventureWorks 檔案](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="oltp-downloads"></a>OLTP 下載

AdventureWorks OLTP 新版的直接連結可在下方：

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>資料倉儲的下載項目

資料倉儲版本之 AdventureWorks 的直接連結可在下方：

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>建立指令碼
下面指令碼可以用來建立整個的 AdventureWorks 資料庫中，而不論版本為何。 

- [AdventureWorks OLTP 指令碼 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW 指令碼 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="install-to-sql-server"></a>安裝 SQL server

### <a name="restore-backup"></a>還原備份
請遵循下列步驟來還原備份的資料庫使用 SQL Server Management Studio。 

1. 開啟 SQL Server Management Studio 並連接至目標 SQL Server 執行個體。
2. 以滑鼠右鍵按一下**資料庫**節點，然後選取**Restore Database**。
3. 選取 **裝置**按一下省略符號 (**...**)
4. 在對話方塊**選取備份裝置**，按一下**新增**，瀏覽至伺服器的檔案系統中的資料庫備份，並選取備份。 按一下 [確定] 。
5. 如有需要變更資料的目標位置，並在記錄檔**檔案**窗格。 請注意，您要放置資料和記錄檔在不同的磁碟機上的最佳作法。
6. 按一下 [確定] 。 這會起始資料庫還原。 完成之後，您必須安裝在您的 SQL Server 執行個體上的 AdventureWorks 資料庫。

如需有關還原 SQL Server 資料庫的詳細資訊，請參閱[還原資料庫備份，使用 SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)。


### <a name="attach-a-datafile"></a>附加的資料檔
請遵循下列步驟將為您使用 SQL Server Management Studio 的資料庫資料檔。

1. 開啟 SQL Server Management Studio 並連接至目標 SQL Server 執行個體。
2. 以滑鼠右鍵按一下**資料庫**節點，然後選取**附加**。
3. 選取 **新增**並瀏覽至。您想要附加的 MDF 檔案。 
1. 選取檔案，然後按一下**確定**。 
    1. 您選取的資料庫應該會顯示在下方視窗。 如果該檔案清單做為 「 找不到 」，選取省略符號 (**...**) 更新的正確路徑的路徑與檔案名稱旁邊。 
    1. 如果您只需要資料檔案 (.mdf) 和不記錄檔 (.ldf)，然後在下方視窗.ldf 反白顯示並選取**移除**。 這會建立新的記錄檔。 
1. 選取 **確定**附加檔案。 將檔案附加之後，您必須安裝在您的 SQL Server 執行個體上的 AdventureWorks 資料庫。  

如需有關附加資料庫檔案的詳細資訊，請參閱 <<c0> [ 附加資料庫](../relational-databases/databases/attach-a-database.md)。 

## <a name="install-to-azure-sql-database"></a>安裝至 Azure SQL Database


如果您還沒有 SQL Server 在 Azure 中，瀏覽至[Azure 入口網站](https://portal.azure.com/)並建立新的 SQL Database。 在進行的建立資料庫，您將建立伺服器。 請記下的伺服器。 請參閱[本教學課程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)分鐘內建立資料庫。

1. 連接到您的 Azure 入口網站。
1. 選取 **建立資源**中左上方的 瀏覽 窗格。 
1. 選取 **資料庫**，然後選取**SQL 資料庫**。 
1. 填寫所需的資訊。
1. 在 **選取來源**欄位中，選取**範例 (AdventureWorksLT)** 還原最新的 AdventureWorksLT 備份的備份。
1. 選取 **建立**來建立新的 SQL Database，也就是 AdventureWorksLT 資料庫的還原的複本。 


## <a name="see-also"></a>另請參閱
[教學課程適用於 SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
[SQL Server database engine 教學課程](../relational-databases/database-engine-tutorials.md)
