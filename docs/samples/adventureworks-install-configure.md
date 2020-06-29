---
title: AdventureWorks 範例資料庫
description: 遵循這些指示，使用 Transact-sql （T-sql）、SQL Server Management Studio （SSMS）或 Azure Data Studio，將 AdventureWorks 範例資料庫下載並安裝到 SQL Server。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/16/2020
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 9f84b6113f9f3904ca65831a00308ab56ee79daa
ms.sourcegitcommit: a0ebbcb717f09d3614de5ce9eb9f3c00f0a45f81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85409237"
---
# <a name="adventureworks-sample-databases"></a>AdventureWorks 範例資料庫
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文提供下載 AdventureWorks 範例資料庫的直接連結，以及將它們還原至 SQL Server 和 Azure SQL Database 的指示。 

如需範例的詳細資訊，請參閱[範例 GitHub 存放庫](https://github.com/microsoft/sql-server-samples/tree/master/samples/databases)。 

## <a name="prerequisites"></a>必要條件

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019)或[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)或[Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)


## <a name="download-bak-files"></a>下載 .bak 檔案 

使用下列連結，為您的案例下載適當的範例資料庫。 

- **OLTP**資料適用于大部分的一般線上交易處理工作負載。 
- 資料倉儲 **（DW）** 資料適用于資料倉儲工作負載。 
- **輕量（LT）** 資料是**OLTP**範例的羽量級和精簡版本。 

|**OLTP** |**資料倉儲** |**輕量型**|
|---------|---------|---------|
|[AdventureWorks2019 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2019.bak)|[AdventureWorksDW2019 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2019.bak)|[AdventureWorksLT2019 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2019.bak)|
|[AdventureWorks2017 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)|[AdventureWorksDW2017 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)|[AdventureWorksLT2017 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2017.bak)|
|[AdventureWorks2016 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)|[AdventureWorksDW2016 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)|[AdventureWorksLT2016 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2016.bak)|
|[AdventureWorks2016_EXT .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016_EXT.bak)|[AdventureWorksDW2016_EXT .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016_EXT.bak)| N/A |
|[AdventureWorks2014 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)|[AdventureWorksDW2014 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)|[AdventureWorksLT2014 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2014.bak)|
|[AdventureWorks2012 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)|[AdventureWorksDW2012 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)|[AdventureWorksLT2012 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2012.bak)|
|[AdventureWorks2008R2 .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)| [AdventureWorksDW2008R2 .bak](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak) | N/A |

您可以直接在 GitHub 上找到其他檔案： 

- [SQL Server 2014-2019](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL Server 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [SQL Server 2008 和2008R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)


## <a name="restore-to-sql-server"></a>還原至 SQL Server 

您可以使用檔案 `.bak` ，將範例資料庫還原至 SQL Server 實例。 您可以使用[RESTORE （transact-sql）](../t-sql/statements/restore-statements-transact-sql.md)命令，或使用[SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)或[Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)中的圖形化介面（GUI）來執行此動作。

# <a name="transact-sql-t-sql"></a>[Transact-SQL (T-SQL)](#tab/tsql)

您可以使用 Transact-sql （T-sql）還原範例資料庫。 以下提供還原 AdventureWorks2019 的範例，但資料庫名稱和安裝檔案路徑可能會根據您的環境而有所不同。 

若要還原 AdventureWorks2019，請將適當的值修改為您的環境，然後執行下列 Transact-sql （T-sql）命令：

```sql
USE [master]
RESTORE DATABASE [AdventureWorks2019] 
FROM  DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\AdventureWorks2019.bak' 
WITH  FILE = 1,  NOUNLOAD,  STATS = 5
GO

```

# <a name="sql-server-management-studio-ssms"></a>[SQL Server Management Studio (SSMS)](#tab/ssms)

如果您不熟悉 SQL Server Management Studio （SSMS），您可以查看[connect & 查詢](../ssms/tutorials/connect-query-sql-server.md)以開始使用。 

若要在 SQL Server Management Studio 中還原資料庫，請遵循下列步驟：

1. `.bak`從[下載 .bak](#download-bak-files)檔案一節中提供的其中一個連結下載適當的檔案。
2. 將檔案移 `.bak` 至您的 SQL Server 備份位置。 這會根據您的安裝位置、實例名稱和 SQL Server 版本而有所不同。 例如，SQL Server 2019 預設實例的預設位置為：

   `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup`. 

3. 開啟 SQL Server Management Studio （SSMS），並連接到中的 SQL Server。 
4. 以滑鼠右鍵**Databases**按一下**物件總管**  >  **還原資料庫 ...** ] 中的 [資料庫]，啟動 [**還原資料庫**]。 

   :::image type="content" source="media/adventureworks-install-configure/restore-db-ssms.png" alt-text="選擇以滑鼠右鍵按一下物件總管中的 [資料庫]，然後選取 [還原資料庫]，以還原資料庫":::


1. 選取 [**裝置**]，然後選取省略號 **（...）** 以選擇裝置。 
1. 選取 [**新增**]，然後選擇 `.bak` 您最近移至此位置的檔案。 如果您已將檔案移到這個位置，但是在嚮導中看不到它，這通常表示許可權問題-SQL Server 或登入 SQL Server 的使用者沒有此資料夾中此檔案的許可權。 
1. 選取 **[確定]** 以確認您的資料庫備份選項，然後關閉 [**選取備份裝置**] 視窗。 
1. 核取 [**檔案] 索引標籤，確認**還原**為**[位置] 和 [檔案名] 符合您在 [**還原資料庫**] 中所需的位置和檔案名。 
1. 選取 [確定]**** 以還原您的資料庫。 

   :::image type="content" source="media/adventureworks-install-configure/restore-db-wizard-ssms.png" alt-text="選擇以滑鼠右鍵按一下物件總管中的 [資料庫]，然後選取 [還原資料庫]，以還原資料庫":::

如需還原 SQL Server 資料庫的詳細資訊，請參閱[使用 SSMS 還原資料庫備份](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)。

# <a name="azure-data-studio"></a>[Azure Data Studio](#tab/data-studio)

如果您不熟悉[Azure Data Studio Studio](../azure-data-studio/download-azure-data-studio.md)，您可以查看[connect & 查詢](../azure-data-studio/quickstart-sql-server.md)以開始使用

若要在 Azure Data Studio 中還原資料庫，請遵循下列步驟：

1. `.bak`從[下載 .bak](#download-bak-files)檔案一節中提供的其中一個連結下載適當的檔案。
1. 將檔案移 `.bak` 至您的 SQL Server 備份位置。 這會根據您的安裝位置、實例名稱和 SQL Server 版本而有所不同。 例如，SQL Server 2019 預設實例的預設位置為：

    `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup`.

1. 開啟 Azure Data Studio Studio 並連接到您的 SQL Server 實例。
1. 在您的伺服器上按一下滑鼠右鍵，然後選取 [**管理**]。

   :::image type="content" source="media/adventureworks-install-configure/ads-manage.png" alt-text="選擇以滑鼠右鍵按一下物件總管中的 [資料庫]，然後選取 [還原資料庫]，以還原資料庫":::

1. 選取**還原**

   :::image type="content" source="media/adventureworks-install-configure/ads-restore-database.png" alt-text="從頂端功能表中選取 [還原]，以還原您的資料庫。":::

1. 在 [**一般**] 索引標籤上，填入 [**來源**] 底下所列的值。
    1. 在 [**還原來源**] 底下，選取 [*備份檔案*]。
    1. 在 [**備份檔案路徑**] 底下，選取您儲存 .bak 檔案的位置。 
    
   :::image type="content" source="media/adventureworks-install-configure/ads-source.png" alt-text="選取您的備份檔案路徑":::
    
    這會自動填入其餘的欄位，例如**資料庫**、**目標資料庫**及**還原至**。 

   :::image type="content" source="media/adventureworks-install-configure/ads-destination-restore-plan.png" alt-text="當您選擇備份檔案路徑之後，其餘的欄位自動填入":::

1. 選取 [**還原**] 以還原您的資料庫。 

   :::image type="content" source="media/adventureworks-install-configure/ads-restore.png" alt-text="準備好之後，請選取 [還原] 以還原您的資料庫。":::

---

## <a name="deploy-to-azure-sql-database"></a>部署至 Azure SQL Database

您有兩個選項可查看範例 Azure SQL Database 資料。 當您建立新的資料庫時，可以使用範例，或者您可以使用 SQL Server Management Studio （SSMS）將資料庫從 SQL Server 直接部署至 Azure。

若要改為取得 Azure SQL 受控執行個體的範例資料，請參閱將[全球匯入工具還原至 SQL 受控執行個體](/azure/azure-sql/managed-instance/restore-sample-database-quickstart)。 

### <a name="deploy-new-sample-database"></a>部署新的範例資料庫

當您在 Azure SQL Database 中建立新資料庫時，可以選擇建立空白資料庫或範例資料庫。 

請遵循下列步驟，使用範例資料庫來建立新的資料庫： 

1. 連接到您的 Azure 入口網站。
1. 選取流覽窗格左上方的 [**建立資源**]。 
1. 選取 [資料庫]****，然後選取 [SQL Database]****。 
1. 填入要求的資訊，以建立您的資料庫。 
1. 在 [**其他設定**] 索引標籤上，選擇 [**範例**] 做為 [**資料來源**] 底下的現有資料： 

   :::image type="content" source="media/adventureworks-install-configure/deploy-sample-to-azure.png" alt-text="建立您的 Azure SQL Database 時，請在 [Azure 入口網站的 [其他設定] 索引標籤上選擇 [範例] 做為資料來源":::

1. 選取 [**建立**] 以建立新的 SQL Database，也就是 AdventureWorksLT 資料庫的還原複本。 


### <a name="deploy-database-from-sql-server"></a>從 SQL Server 部署資料庫

SQL Server Management Studio 提供直接將資料庫部署至 Azure SQL Database 的功能。 這個方法目前不提供資料驗證，因此適用于開發和測試，不應該用於生產環境。 

若要將範例資料庫從 SQL Server 部署至 Azure SQL Database，請遵循下列步驟：

1. 在 SQL Server Management Studio 中連接到您的 SQL Server。 
1. 如果您尚未這麼做，請將[範例資料庫還原至 SQL Server](#restore-to-sql-server)。 
1. 在**物件總管**工作] [  >  **Tasks**  >  **將資料庫部署到 Microsoft Azure SQL Database**] 中，以滑鼠右鍵按一下您還原的資料庫。 

   :::image type="content" source="media/adventureworks-install-configure/deploy-db-to-azure.png" alt-text="選擇要將您的資料庫部署至 Microsoft Azure SQL Database，方法是以滑鼠右鍵按一下您的資料庫，然後選取 [工作]":::

1. 依照嚮導的指示，連接到 Azure SQL Database 並部署您的資料庫。 


## <a name="creation-scripts"></a>建立腳本

除了還原資料庫，您可以使用腳本來建立 AdventureWorks 資料庫，而不論版本為何。 

下列腳本可以用來建立整個 AdventureWorks 資料庫： 

- [AdventureWorks OLTP 腳本 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW 腳本 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

有關使用腳本的其他資訊，可以在[GitHub](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)上找到。 

## <a name="next-steps"></a>後續步驟

還原範例資料庫之後，請使用下列教學課程來開始使用 SQL Server： 


[SQL Server 資料庫引擎的教學課程](../relational-databases/database-engine-tutorials.md)   
[使用 SQL Server Management Studio （SSMS）進行連線和查詢](../ssms/tutorials/connect-query-sql-server.md)   
[使用 Azure Data Studio 連接及查詢](../ssms/tutorials/connect-query-sql-server.md)