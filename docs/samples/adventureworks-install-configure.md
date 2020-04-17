---
title: 安裝並設定 AdventureWorks 範例資料庫
description: 按照這些說明下載和安裝 AdventureWorks 範例資料庫與 SQL 伺服器管理工作室或 Azure SQL 資料庫中。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 7fa3d199450750a444f2b67ae3e4583549d449b9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484567"
---
# <a name="adventureworks-installation-and-configuration"></a>AdventureWorks 的安裝和設定
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks 下載連結和安裝說明。 

## <a name="prerequisites"></a>Prerequisites

- [SQL 伺服器](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)或[Azure SQL 資料庫](https://azure.microsoft.com/services/sql-database/)。 對於範例的完整版本,請使用 SQL 伺服器評估/開發人員/企業版。
- [SQL 伺服器管理工作室](../ssms/download-sql-server-management-studio-ssms.md)。 為獲得最佳效果,請使用 2016 年 6 月版本或更高版本。
 
## <a name="oltp-downloads"></a>OLTP 下載

直接連結到的OLTP版本的冒險工廠可以找到如下:

- [冒險工廠2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [冒險工廠2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [冒險工廠2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [冒險工廠2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [冒險工廠2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>資料倉儲下載

指向 AdventureWorks 的資料主目錄版本的直接連結,如下所示:

- [冒險工廠DW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [冒險工廠DW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [冒險工廠DW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [冒險工廠DW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [冒險工廠DW2008R2.bak](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak)

## <a name="creation-scripts"></a>建立文稿
以下腳本可用於創建整個 AdventureWorks 資料庫,而不考慮版本。 

- [冒險工廠OLTP文稿Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [冒險工廠 DW 文稿 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="github-links"></a>GitHub 連結

- [SQL 2014 - 2016 的所有 AdventureWorks 檔案](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL 2012 的所有 AdventureWorks 檔案](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [SQL 2008 與 2008R2 的所有 AdventureWorks 檔案](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="install-to-sql-server"></a>安裝到 SQL 伺服器

### <a name="restore-backup"></a>回復備份
按照以下步驟使用 SQL 伺服器管理工作室還原資料庫的備份。 

1. 打開 SQL 伺服器管理工作室並連接到目標 SQL Server 實例。
2. 右鍵單擊**資料庫**節點,然後選擇 **「還原資料庫**」。。
3. 選擇**裝置裝置「 並**按下橢圓 (**...**)
4. 在對話框中選擇**備份設備**,按一下「**添加**」,導航到伺服器檔系統中的資料庫備份,然後選擇備份。 按一下 [確定]  。
5. 如果需要,請更改「**檔」** 窗格中資料和紀錄檔的目標位置。 請注意,最佳做法是將數據和日誌檔放在不同的驅動器上。
6. 按一下 [確定]  。 這將啟動資料庫還原。 完成後,您將在 SQL Server 實例上安裝 AdventureWorks 資料庫。

有關還原 SQL Server 資料庫的詳細資訊,請參閱[使用 SSMS 還原資料庫備份](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)。


### <a name="attach-a-datafile"></a>附加資料檔案
按照以下步驟使用 SQL 伺服器管理工作室附加資料庫的數據檔。

1. 打開 SQL 伺服器管理工作室並連接到目標 SQL Server 實例。
2. 右鍵按下 **「資料庫」** 節點,然後選擇 **「附加**」。
3. 選擇 **「添加**並導航到 」。要附加的 MDF 檔。 
1. 選取檔案，然後按一下 [確定] ****。 
    1. 您選擇的資料庫應顯示在底部視窗中。 如果檔列為"未找到",請選擇檔名旁邊的省略號 (**...),** 並將路徑更新為正確的路徑。 
    1. 如果只有資料檔 (.mdf),而不是日誌檔 (.ldf),則突出顯示底部視窗中的 .ldf 並選擇 **"刪除**"。 這將創建新的日誌檔。 
1. 選擇 **「確定」** 以附加檔。 附加檔案後,您將在 SQL Server 實例上安裝 AdventureWorks 資料庫。  

有關附加資料庫檔案的詳細資訊,請參考[額外資料庫](../relational-databases/databases/attach-a-database.md)。 

## <a name="install-to-azure-sql-database"></a>安裝到 Azure SQL 資料庫


如果 Azure 中尚未有 SQL 伺服器,請導航到[Azure 門戶](https://portal.azure.com/)並創建新的 SQL 資料庫。 在建立資料庫的過程中,您將創建一個伺服器。 記下伺服器。 請參閱[本教程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/),在幾分鐘內創建資料庫。

1. 連接到 Azure 門戶。
1. 選擇 **「在**導航窗格左上角建立資源」。 
1. 選取 [資料庫]****，然後選取 [SQL Database]****。 
1. 填寫所需的資訊。
1. 在**選擇來源**欄位中,選擇 **「範例」(AdventureWorksLT)** 以回復最新 AdventureWorksLT 備份的備份。
1. 選擇 **"創建**"以建立新的 SQL 資料庫,該資料庫是 AdventureWorksLT 資料庫的還原副本。 


## <a name="see-also"></a>另請參閱
[SQL 伺服器管理工作室教學](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[SQL Server 資料庫引擎教學](../relational-databases/database-engine-tutorials.md)
