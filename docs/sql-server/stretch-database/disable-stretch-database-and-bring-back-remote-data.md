---
title: 停用 Stretch Database 並帶回遠端資料 | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, disabling
- disabling Stretch Database
ms.assetid: c1bbb24e-47e3-46aa-b786-fcadf9fb65ce
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: dbfe0a9f6927e1dd62469c8d3e7c3be542cbda76
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794806"
---
# <a name="disable-stretch-database-and-bring-back-remote-data"></a>停用 Stretch Database 並帶回遠端資料
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  若要停用資料表的 Stretch Database，請在 SQL Server Management Studio 中針對資料表選取 [延展]  。 然後選取下列其中一個選項。  
  
-   **停用 | 從 Azure 回復資料**。 將資料表遠端資料從 Azure 複製回 SQL Server，然後再停用資料表的 Stretch Database。 此作業會產生資料傳輸成本，且無法取消。  
  
-   **停用 | 將資料保留在 Azure**。 停用資料庫的 Stretch Database 。  放棄位於 Azure 的資料表遠端資料。  
  
 您也可以使用 Transact-SQL 來為資料表或資料庫停用 Stretch Database。  
  
 針對資料表停用 Stretch Database 後，即會停止執行資料移轉作業，且查詢結果不再包含來自遠端資料表的結果。  
  
 如果您只想暫停資料移轉，請參閱 [暫停和繼續資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)。  
  
> [!NOTE]
> 針對資料表或資料庫停用 Stretch Database，並不會刪除遠端物件。 若您想要刪除遠端資料表或遠端資料庫，則必須使用 Azure 管理入口網站將其卸除。 遠端物件會繼續產生 Azure 成本，直到您將其刪除為止。 如需詳細資訊，請參閱 [SQL Server Stretch Database 定價](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
## <a name="disable-stretch-database-for-a-table"></a>停用資料表的 Stretch Database  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-table"></a>使用 SQL Server Management Studio 停用資料表的 Stretch Database  
  
1.  在 SQL Server Management Studio 的 [物件總管] 中，選取您要停用 Stretch Database 的資料表。  
  
2.  按一下滑鼠右鍵並選取 [Stretch]，然後選取下列其中一個選項。  
  
    -   **停用 | 從 Azure 回復資料**。 將資料表遠端資料從 Azure 複製回 SQL Server，然後再停用資料表的 Stretch Database。 無法取消此命令。  
  
        > [!NOTE]
        > 將資料表的遠端資料從 Azure 複製回 SQL Server 會產生資料傳輸成本。 如需詳細資訊，請參閱 [資料傳輸定價詳細資料](https://azure.microsoft.com/pricing/details/data-transfers/)。  
  
         將所有遠端資料從 Azure 複製回 SQL Server 後，即會針對資料表停用 Stretch。  
  
    -   **停用 | 將資料保留在 Azure**。 停用資料庫的 Stretch Database 。  放棄位於 Azure 的資料表遠端資料。  
  
    > [!NOTE]
    > 針對資料表停用 Stretch Database，並不會刪除遠端資料或遠端資料表。 若您想要刪除遠端資料表，則必須使用 Azure 管理入口網站將其卸除。 遠端資料表會繼續產生 Azure 成本，直到您將其刪除為止。 如需詳細資訊，請參閱 [SQL Server Stretch Database 定價](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-table"></a>使用 Transact-SQL 來為資料表停用 Stretch Database  
  
-   若要針對資料表停用 Stretch，並將資料表的遠端資料從 Azure複製回 SQL Server，請執行下列命令。將所有遠端資料從 Azure 複製回 SQL Server 後，即會針對資料表停用 Stretch。

    無法取消此命令。  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ; 
    GO 
    ```  
  
    > [!NOTE]
    > 將資料表的遠端資料從 Azure 複製回 SQL Server 會產生資料傳輸成本。 如需詳細資訊，請參閱 [資料傳輸定價詳細資料](https://azure.microsoft.com/pricing/details/data-transfers/)。    
  
-   若要針對資料表停用 Stretch 並放棄遠端資料，請執行下列命令。  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ; 
    GO
    ```  
  
> [!NOTE]
> 針對資料表停用 Stretch Database，並不會刪除遠端資料或遠端資料表。 若您想要刪除遠端資料表，則必須使用 Azure 管理入口網站將其卸除。 遠端資料表會繼續產生 Azure 成本，直到您將其刪除為止。 如需詳細資訊，請參閱 [SQL Server Stretch Database 定價](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
## <a name="disable-stretch-database-for-a-database"></a>為資料庫停用 Stretch Database  
 針對資料庫停用 Stretch Database 前，您必須針對資料庫中個別啟用 Stretch 的資料表停用 Stretch Database。  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-database"></a>使用 SQL Server Management Studio 停用資料庫的 Stretch Database  
  
1.  在 SQL Server Management Studio 的 [物件總管] 中，選取您要停用 Stretch Database 的資料庫。  
  
2.  按一下滑鼠右鍵並選取 [工作]，然後選取 [Stretch]，再選取 [停用]。  
  
> [!NOTE]
> 針對資料庫停用 Stretch Database，並不會刪除遠端資料庫。 若您想要刪除遠端資料庫，則必須使用 Azure 管理入口網站將其卸除。 遠端資料庫會繼續產生 Azure 成本，直到您將其刪除為止。 如需詳細資訊，請參閱 [SQL Server Stretch Database 定價](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-database"></a>使用 Transact-SQL 來為資料庫停用 Stretch Database  
 執行下列命令。  
  
```sql  
ALTER DATABASE <Stretch-enabled database name>  
    SET REMOTE_DATA_ARCHIVE = OFF ;  
GO 
```  
  
> [!NOTE]
> 針對資料庫停用 Stretch Database，並不會刪除遠端資料庫。 若您想要刪除遠端資料庫，則必須使用 Azure 管理入口網站將其卸除。 遠端資料庫會繼續產生 Azure 成本，直到您將其刪除為止。 如需詳細資訊，請參閱 [SQL Server Stretch Database 定價](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [暫停和繼續資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
  
