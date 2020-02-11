---
title: 安裝和設定 AdventureWorks 範例資料庫
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 6a4b56a31ede0d8e011c1a2244f5d014e185e7e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74318989"
---
# <a name="adventureworks-installation-and-configuration"></a>AdventureWorks 安裝和設定
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks 下載連結和安裝指示。 

## <a name="prerequisites"></a>Prerequisites

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)或[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 如需完整版本的範例，請使用 SQL Server Evaluation/Developer/Enterprise Edition。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 若要獲得最佳結果，請使用2016年6月版本或更新版本。
 
## <a name="oltp-downloads"></a>OLTP 下載

您可以在下面找到有關 AdventureWorks OLTP 版本的直接連結：

- [AdventureWorks2017 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>資料倉儲下載

您可以在下面找到 AdventureWorks 資料倉儲版本的直接連結：

- [AdventureWorksDW2017 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>建立腳本
您可以使用下列腳本來建立整個 AdventureWorks 資料庫，而不考慮版本。 

- [AdventureWorks OLTP 腳本 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW 腳本 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="github-links"></a>GitHub 連結

- [SQL 2014-2016 的所有 AdventureWorks 檔案](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL 2012 的所有 AdventureWorks 檔案](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [適用于 SQL 2008 和2008R2 的所有 AdventureWorks 檔案](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="install-to-sql-server"></a>安裝至 SQL Server

### <a name="restore-backup"></a>還原備份
請遵循下列步驟，使用 SQL Server Management Studio 來還原資料庫的備份。 

1. 開啟 SQL Server Management Studio，並連接到目標 SQL Server 實例。
2. 以滑鼠右鍵按一下 [**資料庫**] 節點，然後選取 [**還原資料庫**]。
3. 選取 [**裝置**]，然後按一下省略號（**...**）
4. 在對話方塊中，**選取 [備份裝置**]，按一下 [**新增**]，流覽至伺服器檔案系統中的資料庫備份，然後選取備份。 按一下 [確定]  。
5. 如有需要，請在 [檔案] 窗格中變更**資料檔案和**記錄檔的目標位置。 請注意，最佳做法是將資料和記錄檔放在不同的磁片磁碟機上。
6. 按一下 [確定]  。 這會起始資料庫還原。 完成之後，您的 SQL Server 實例上會安裝 AdventureWorks 資料庫。

如需還原 SQL Server 資料庫的詳細資訊，請參閱[使用 SSMS 還原資料庫備份](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)。


### <a name="attach-a-datafile"></a>附加資料檔案
請遵循下列步驟，使用 SQL Server Management Studio 附加資料庫的資料檔案。

1. 開啟 SQL Server Management Studio，並連接到目標 SQL Server 實例。
2. 以滑鼠右鍵按一下 [**資料庫**] 節點，然後選取 [**附加**]。
3. 選取 [**新增**]，並流覽至。您想要附加的 .MDF 檔案。 
1. 選取檔案，然後按一下 [確定] ****。 
    1. 您所選取的資料庫應該會顯示在下方視窗中。 如果檔案列為「找不到」，請選取檔案名旁邊的省略號（**...**），並將路徑更新為正確的路徑。 
    1. 如果您只有資料檔（.mdf），而不是記錄檔（.ldf），請反白顯示底部視窗中的 .ldf，然後選取 [**移除**]。 這會建立新的記錄檔。 
1. 選取 **[確定]** 以附加檔案。 附加檔案之後，您的 SQL Server 實例上會安裝 AdventureWorks 資料庫。  

如需附加資料庫檔案的詳細資訊，請參閱[附加資料庫](../relational-databases/databases/attach-a-database.md)。 

## <a name="install-to-azure-sql-database"></a>安裝至 Azure SQL Database


如果您在 Azure 中還沒有 SQL Server，請流覽至 [ [Azure 入口網站](https://portal.azure.com/)]，然後建立新的 SQL Database。 在建立資料庫的過程中，您將會建立伺服器。 請記下伺服器。 請參閱[此教學](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)課程，以在短短幾分鐘內建立資料庫。

1. 連接到您的 Azure 入口網站。
1. 選取流覽窗格左上方的 [**建立資源**]。 
1. 選取 [資料庫]****，然後選取 [SQL Database]****。 
1. 填寫所需的資訊。
1. 在 [**選取來源**] 欄位中，選取 [**範例（AdventureWorksLT）** ] 以還原最新 AdventureWorksLT 備份的備份。
1. 選取 [**建立**] 以建立新的 SQL Database，也就是 AdventureWorksLT 資料庫的還原複本。 


## <a name="see-also"></a>另請參閱
[SQL Server Management Studio 的教學課程](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[SQL Server 資料庫引擎的教學課程](../relational-databases/database-engine-tutorials.md)
