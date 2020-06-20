---
title: 建立資料庫快照集 (Transact-SQL) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], creating
ms.assetid: 187fbba3-c555-4030-9bdf-0f01994c5230
author: stevestein
ms.author: sstein
ms.openlocfilehash: bae68c2d507e1dd3809e76a9d842b765d72234e9
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84952087"
---
# <a name="create-a-database-snapshot-transact-sql"></a>建立資料庫快照集 (Transact-SQL)
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是建立 [!INCLUDE[tsql](../../includes/tsql-md.md)]資料庫快照集的唯一方式。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 不支援建立資料庫快照集。  
  
-   **開始之前：**  
  
     [先決條件](#Prerequisites)  
  
     [安全性](#Security)  
  
     [最佳作法：命名資料庫快照集](#Naming)  
  
-   **若要建立資料庫快照集，請使用：**  [transact-sql](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 可使用任何復原模式的來源資料庫必須符合下列必要條件：  
  
-   伺服器執行個體必須執行支援資料庫快照集的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 如需中資料庫快照集支援的詳細資訊 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，請參閱[SQL Server 2014 版本支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
-   除非來源資料庫是資料庫鏡像工作階段中的鏡像資料庫，否則該資料庫必須處於線上狀態。  
  
-   若要在鏡像資料庫上建立資料庫快照集，資料庫必須處於同步處理的[鏡像狀態](../../database-engine/database-mirroring/mirroring-states-sql-server.md)。  
  
-   來源資料庫無法設定為可擴充的共用資料庫。  
  
> [!IMPORTANT]  
>  如需其他重要考量的資訊，請參閱 [資料庫快照集 &#40;SQL Server&#41;](database-snapshots-sql-server.md)資料庫快照集的唯一方式。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
 本節討論下列最佳作法：  
  
-   [最佳作法：命名資料庫快照集](#Naming)  
  
-   [最佳作法：限制資料庫快照集的數目](#Limiting_Number)  
  
-   [最佳作法：用戶端連接到資料庫快照集](#Client_Connections)  
  
####  <a name="best-practice-naming-database-snapshots"></a><a name="Naming"></a>最佳做法：命名資料庫快照集  
 建立快照集之前，務必先考慮如何命名快照集。 每個資料庫快照集都需要一個唯一的資料庫名稱。 為了方便管理，快照集的名稱可加入用於識別資料庫的資訊，例如：  
  
-   來源資料庫的名稱。  
  
-   表明新名稱是用於快照集的指示。  
  
-   建立快照集的日期和時間、序號或其他資訊 (例如一天中的時間)，以便區隔給定資料庫上的循序快照集。  
  
 例如，假設 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫有一系列的快照集， 三個每日快照集依據 24 小時制，以 6 小時為間隔，從早上 6 點 到下午 6 點間分別建立。 每個每日快照集在卸除並被相同名稱的新快照集取代之前，會先保留 24 小時。 注意下列快照集名稱，每個都表示時間 (小時)，而非日期：  
  
```  
AdventureWorks_snapshot_0600  
AdventureWorks_snapshot_1200  
AdventureWorks_snapshot_1800  
```  
  
 或者，如果每天建立這些每日快照集的時間會變動，則最好採用一個較籠統的命名慣例，例如：  
  
```  
AdventureWorks_snapshot_morning  
AdventureWorks_snapshot_noon  
AdventureWorks_snapshot_evening  
```  
  
####  <a name="best-practice-limiting-the-number-of-database-snapshots"></a><a name="Limiting_Number"></a> 最佳作法：限制資料庫快照集的數目  
 隨時間建立一系列的快照集，可擷取來源資料庫的循序快照集。 每個快照集都會一直保存到確實卸除該快照集為止。 因為每個快照集都會隨著原始頁面更新而不斷成長，所以您可能想要在建立新快照集之後，刪除較早的快照集，以節省磁碟空間。  
  
> [!NOTE]  
>  若要還原為資料庫快照集，您需要刪除該資訊庫中的任何其他快照集。  
  
####  <a name="best-practice-client-connections-to-a-database-snapshot"></a><a name="Client_Connections"></a> 最佳作法：用戶端連接到資料庫快照集  
 若要使用資料庫快照集，用戶端需要知道去哪裡尋找。 正在建立或刪除某個資料庫快照集時，使用者仍可讀取其他快照集。 但是，當您以新的快照集取代現有的快照集時，必須將用戶端重新導向至新的快照集。 使用者可以利用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，手動連接到資料庫快照集。 但是，若要支援實際執行環境，您應該建立程式設計方案，將撰寫報表的用戶端明確導向至資料庫最新的資料庫快照集。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 能夠建立資料庫的任何使用者都可以建立資料庫快照集，不過若要建立鏡像資料庫的快照集，您必須是 **sysadmin** 固定伺服器角色的成員。  
  
##  <a name="how-to-create-a-database-snapshot-using-transact-sql"></a><a name="TsqlProcedure"></a> 如何建立資料庫快照集 (使用 Transact-SQL)  
 **若要建立資料庫快照集**  
  
> [!NOTE]  
>  如需此程序的範例，請參閱本節稍後的 [範例 (Transact-SQL)](#TsqlExample)。  
  
1.  根據來源資料庫的目前大小，確定您擁有足夠的磁碟空間可存放資料庫快照集。 資料庫快照集的大小上限為快照集建立時的來源資料庫大小。 如需詳細資訊，請參閱[檢視資料庫快照集的疏鬆檔案大小 &#40;Transact-SQL&#41;](view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)。  
  
2.  在使用 AS SNAPSHOT OF 子句的檔案上，發出 CREATE DATABASE 陳述式。 建立快照集必須指定來源資料庫之每個資料庫檔案的邏輯名稱。 語法如下所示：  
  
     CREATE DATABASE *database_snapshot_name*  
  
     開啟  
  
     (  
  
     名稱 =*logical_file_name*，  
  
     FILENAME ='*os_file_name*'  
  
     ) [ ,...*n* ]  
  
     AS SNAPSHOT OF *source_database_name*  
  
     [;]  
  
     其中*source_ * * database_name*是源資料庫， *logical_file_name*在參考檔案時 SQL Server 中使用的邏輯名稱， *os_file_name*是當您建立檔案時，作業系統所使用的路徑和檔案名，而*database_snapshot_name*則是您要還原資料庫的目標快照集名稱。 如需此語法的完整描述，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)資料庫快照集的唯一方式。  
  
    > [!NOTE]  
    >  建立資料庫快照集時，CREATE DATABASE 陳述式中不允許記錄檔、離線檔案、還原檔案與無用檔案。  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 範例 (Transact-SQL)  
  
> [!NOTE]  
>  用於範例中的 `.ss` 副檔名可自行決定。  
  
 本區段包含下列範例：  
  
-   A. [在 AdventureWorks 資料庫上建立快照集](#Creating_on_AW)  
  
-   B. [在 Sales 資料庫上建立快照集](#Creating_on_Sales)  
  
####  <a name="a-creating-a-snapshot-on-the-adventureworks-database"></a><a name="Creating_on_AW"></a> A. 在 AdventureWorks 資料庫上建立快照集  
 此範例會在 `AdventureWorks` 資料庫上建立資料庫快照集。 快照集名稱 `AdventureWorks_dbss_1800`與疏鬆檔案的檔案名稱 `AdventureWorks_data_1800.ss`，表示建立時間是 6 P.M (1800 小時)。  
  
```  
CREATE DATABASE AdventureWorks_dbss1800 ON  
( NAME = AdventureWorks_Data, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data\AdventureWorks_data_1800.ss' )  
AS SNAPSHOT OF AdventureWorks;  
GO  
```  
  
####  <a name="b-creating-a-snapshot-on-the-sales-database"></a><a name="Creating_on_Sales"></a> B. 在 Sales 資料庫上建立快照集  
 此範例會在 `sales_snapshot1200`資料庫上建立資料庫快照集 `Sales` 。 此資料庫是在[建立資料庫 &#40;SQL Server transact-sql&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)中的「建立含有檔案群組的資料庫」範例中所建立。  
  
```  
--Creating sales_snapshot1200 as snapshot of the  
--Sales database:  
CREATE DATABASE sales_snapshot1200 ON  
( NAME = SPri1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SPri1dat_1200.ss'),  
( NAME = SPri2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SPri2dt_1200.ss'),  
( NAME = SGrp1Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\mssql\data\SG1Fi1dt_1200.ss'),  
( NAME = SGrp1Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SG1Fi2dt_1200.ss'),  
( NAME = SGrp2Fi1_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SG2Fi1dt_1200.ss'),  
( NAME = SGrp2Fi2_dat, FILENAME =   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\data\SG2Fi2dt_1200.ss')  
AS SNAPSHOT OF Sales;  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [檢視資料庫快照集 &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [將資料庫還原成資料庫快照集](revert-a-database-to-a-database-snapshot.md)  
  
-   [卸除資料庫快照集 &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [資料庫快照集 &#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
