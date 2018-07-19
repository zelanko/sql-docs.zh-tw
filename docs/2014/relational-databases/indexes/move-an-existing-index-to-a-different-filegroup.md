---
title: 將現有的索引移至不同的檔案群組 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- moving tables
- switching filegroups for index
- moving indexes
- indexes [SQL Server], moving
- filegroups [SQL Server], switching
ms.assetid: 167ebe77-487d-4ca8-9452-4b2c7d5cb96e
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 597ed7b2207302ff897f255479c6183ef44b255d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285164"
---
# <a name="move-an-existing-index-to-a-different-filegroup"></a>將現有的索引移至不同的檔案群組
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中將目前檔案群組的現有索引移到不同的檔案群組。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要將現有的索引移至不同的檔案群組，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果資料表含有叢集索引，則將叢集索引移到新的檔案群組也會使資料表移到該檔案群組中。  
  
-   您無法使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]移動使用 UNIQUE 或 PRIMARY KEY 條件約束建立的索引。 若要移動這些索引，請使用 [中的](/sql/t-sql/statements/create-index-transact-sql) CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式搭配 (DROP_EXISTING=ON) 選項。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-using-table-designer"></a>若要使用資料表設計工具將現有的索引移至不同的檔案群組  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含的資料表中有您要移動的索引。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  以滑鼠右鍵按一下包含您要移動之索引的資料表，然後選取 [設計]。  
  
4.  在 [資料表設計工具] 功能表上，按一下 [索引/索引鍵]。  
  
5.  選取您要移動的索引。  
  
6.  在主要方格中，展開 **[資料空間規格]**。  
  
7.  選取 **[檔案群組或分割區配置名稱]** ，然後從清單中選取要將索引移至其中的檔案群組或分割區配置。  
  
8.  按一下 [ **關閉**]。  
  
9. 在 [檔案] 功能表上，選取 [儲存 <資料表名稱>]。  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-in-object-explorer"></a>若要在物件總管中將現有的索引移到不同的檔案群組  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含的資料表中有您要移動的索引。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號，展開包含您要移動之索引的資料表。  
  
4.  按一下加號展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下您要移動的索引，然後選取 [屬性]。  
  
6.  在 **[選取頁面]** 底下，選取 **[儲存體]**。  
  
7.  選取要移動索引的檔案群組。  
  
     如果資料表或索引已分割，請選取移動索引所使用的分割區配置。 如需有關分割區索引的詳細資訊，請參閱＜ [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)＞。  
  
     如果您要移動叢集索引，可使用線上處理。 線上處理允許並行使用者在索引作業期間，存取基礎資料和非叢集索引。 如需詳細資訊，請參閱 [Perform Index Operations Online](perform-index-operations-online.md)。  
  
     在使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的多處理器電腦上，您可以指定平行處理原則的最大程度值，藉以設定用來執行索引陳述式的處理器數目。 並非每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]版本都可使用平行索引作業功能。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。 如需平行索引作業的詳細資訊，請參閱 [設定平行索引作業](configure-parallel-index-operations.md)。  
  
8.  按一下 **[確定]**。  
  
 下列資訊可從 [索引屬性 - *index_name*] 對話方塊的 [儲存體] 頁面取得：  
  
 **檔案群組**  
 在指定的檔案群組中儲存索引。 清單僅顯示標準 (資料列) 檔案群組。 預設清單選取項目為資料庫的 PRIMARY 檔案群組。  
  
 **檔案資料流檔案群組**  
 為 FILESTREAM 資料指定檔案群組。 此清單只會顯示 FILESTREAM 檔案群組。 預設清單選取項目為資料庫的 PRIMARY FILESTREAM 檔案群組。  
  
 **分割區配置**  
 在資料分割結構描述中儲存索引。 按一下 **[資料分割配置]** 以啟用下列方格。 預設清單選取項目是用來儲存資料表資料的資料分割配置。 當您在清單中選取不同的資料分割配置時，會更新方格中的資訊。  
  
 如果資料庫中沒有資料分割結構描述，則無法使用資料分割結構描述選項。  
  
 **檔案資料流資料分割配置**  
 指定資料分割配置的 FILESTREAM 資料。 資料分割配置必須對稱於在 **[資料分割配置]** 選項中所指定的配置。  
  
 如果資料表不是資料分割，則此欄位空白。  
  
 **資料分割結構描述參數**  
 顯示參與資料分割結構描述的資料行名稱。  
  
 **資料表資料行**  
 選取資料表或檢視以對應至資料分割結構描述。  
  
 **資料行資料類型**  
 顯示有關資料行的資料類型資訊。  
  
> [!NOTE]  
>  如果資料表資料行是計算資料行， **[資料行資料類型]** 就會顯示「計算資料行」。  
  
 **移動索引時，允許線上處理 DML 陳述式**  
 允許使用者在索引作業期間存取基礎資料表或叢集索引資料，以及與非叢集索引相關聯的任何項目。  
  
> [!NOTE]  
>  此選項不適用於 XML 索引，或索引為已停用的叢集索引時亦不適用。  
  
 **設定最大平行程度**  
 限制平行計畫執行期間要使用的處理器數目。 預設值 (0) 會使用實際可用的 CPU 數目。 將值設定為 1 會抑制平行計畫的產生；將值設定為大於 1 的數字則會限制單一查詢執行所使用的處理器最大數目。 此選項僅會在對話方塊處於 **[重建]** 或 **[重新建立]** 狀態時可用。  
  
> [!NOTE]  
>  如果指定的數值大於可用的 CPU 數目，就會使用可用 CPU 的實際數目。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup"></a>若要將現有的索引移至不同的檔案群組  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the TransactionsFG1 filegroup on the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP TransactionsFG1;  
    GO  
    /* Adds the TransactionsFG1dat3 file to the TransactionsFG1 filegroup. Please note that you will have to change the filename parameter in this statement to execute it without errors.  
    */  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = TransactionsFG1dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\TransactionsFG1dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP TransactionsFG1;  
    GO  
    /*Creates the IX_Employee_OrganizationLevel_OrganizationNode index  
      on the TransactionsPS1 filegroup and drops the original IX_Employee_OrganizationLevel_OrganizationNode index.  
    */  
    CREATE NONCLUSTERED INDEX IX_Employee_OrganizationLevel_OrganizationNode  
        ON HumanResources.Employee (OrganizationLevel, OrganizationNode)  
        WITH (DROP_EXISTING = ON)  
        ON TransactionsFG1;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)。  
  
  
