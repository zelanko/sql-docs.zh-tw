---
title: 建立叢集索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index creation [SQL Server], clustered indexes
- clustered indexes, creating
- clustered indexes, PRIMARY KEY constraint
- clustered indexes, UNIQUE constraint
- indexes [SQL Server], clustered
ms.assetid: 47148383-c2c7-4f08-a9e4-7016bf2d1d13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3cea4731ee665e401429679d764832247b2a2242
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63155377"
---
# <a name="create-clustered-indexes"></a>建立叢集索引
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的資料表上建立叢集索引。 除了極少數的例外狀況之外，每個資料表都應該要有叢集索引。 除了可以改善查詢效能以外，叢集索引還能夠視需要加以重建或重新組織，以便控制資料表分散程度。 檢視上也可以建立叢集索引。 (叢集索引是在 [叢集與非叢集索引說明](clustered-and-nonclustered-indexes-described.md)主題中進行定義。)  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [一般實作](#Implementations)  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法在資料表上建立叢集索引：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Implementations"></a> 一般實作  
 實作叢集索引的方法如下：  
  
-   **PRIMARY KEY 與 UNIQUE 條件約束**  
  
     建立 PRIMARY KEY 條件約束時，若資料表上沒有存在叢集索引，而且您未指定唯一的非叢集索引，則資料行上會自動建立唯一的叢集索引。 主索引鍵資料行不允許 NULL 值。  
  
     當您建立 UNIQUE 條件約束時，依預設會建立唯一的非叢集索引，以強制 UNIQUE 條件約束。 若資料表上還沒有叢集索引，您可以指定唯一叢集索引。  
  
     隨條件約束一起建立的索引，會自動採用與條件約束名稱相同的名稱。 如需相關資訊，請參閱 [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md) 及 [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md)。  
  
-   **獨立於條件限制之外的索引**  
  
     如果已指定非叢集的主索引鍵條件約束，您可以在主索引鍵資料行以外的資料行上建立叢集索引。  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   建立叢集索引結構時，個別的檔案和檔案群組中都必須有磁碟空間來保存舊 (來源) 結構和新 (目標) 結構。 除非認可整個交易，否則舊結構的配置不會取消。 此外，可能還需要額外的暫存磁碟空間以供排序之用。 如需詳細資訊，請參閱 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)。  
  
-   若叢集的索引建立於含多個現有非叢集索引的堆積上，所有的非叢集索引都必須重建，以便讓它們包含叢集索引鍵值，而非資料列識別碼 (RID)。 同樣地，若擁有多個非叢集索引之資料表上的叢集索引被卸除了，非叢集索引將會全部重建，做為 DROP 作業的一部份。 在大型資料表中，這可能會花許多時間。  
  
     在大型資料表上建立索引的較佳方式是以叢集索引開始，然後建立任何非叢集索引。 當您在現有資料表上建立索引時，請考慮將 ONLINE 選項設定為 ON。 設定為 ON 時，將不會長期鎖定資料表。 這樣一來，基礎資料表上就可以繼續執行查詢或更新動作。 如需詳細資訊，請參閱 [Perform Index Operations Online](perform-index-operations-online.md)。  
  
-   叢集索引的索引鍵所包含的 `varchar` 資料行不能在 ROW_OVERFLOW_DATA 配置單位中有現有的資料。 如果在 `varchar` 資料行上建立叢集索引，且現有的資料在 IN_ROW_DATA 配置單位中，則後續在可能發送資料非資料列的資料行上進行的插入或更新動作會失敗。 若要取得可能包含資料列溢位資料之資料表的相關資訊，請使用 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql) 動態管理函數。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-clustered-index-by-using-object-explorer"></a>若要使用物件總管建立叢集索引  
  
1.  在 [物件總管] 中，展開要在其中建立叢集索引的資料表。  
  
2.  以滑鼠右鍵按一下 [索引]  資料夾，指向 [新增索引]  ，然後選取 [叢集索引…]  。  
  
3.  在 **[新增索引]** 對話方塊，於 **[一般]** 頁面上的 **[索引名稱]** 方塊中輸入新索引的名稱。  
  
4.  按一下 [索引鍵資料行]  下的 [新增...]  。  
  
5.  在 [**從**_Table_name_選取資料行] 對話方塊中，選取要加入至叢集索引之資料表資料行的核取方塊。  
  
6.  按一下 [確定]  。  
  
7.  在 **[新增索引]** 對話方塊中，按一下 **[確定]** 。  
  
#### <a name="to-create-a-clustered-index-by-using-the-table-designer"></a>若要使用資料表設計工具建立叢集索引  
  
1.  在 [物件總管] 中，展開要在其中建立包含叢集索引之資料表的資料庫。  
  
2.  以滑鼠右鍵按一下 [資料表]  資料夾，然後按一下 [新增資料表…]  。  
  
3.  像平常一樣，建立新資料表。 如需詳細資訊，請參閱[建立資料表 &#40;Database Engine&#41;](../tables/create-tables-database-engine.md)。  
  
4.  以滑鼠右鍵按一下上面建立的新資料表，然後按一下 [設計]  。  
  
5.  在 [資料表設計工具]  功能表上，按一下 [索引/索引鍵]  。  
  
6.  在 [索引/索引鍵]  對話方塊中，按一下 [加入]  。  
  
7.  從 [選取的主索引鍵/唯一索引鍵或索引]  文字方塊中選取新索引。  
  
8.  在方格中，選取 [建立成 CLUSTERED]  ，然後從屬性右邊的下拉式清單中選擇 [是]  。  
  
9. 按一下 [關閉]  。  
  
10. **在 [檔案**] 功能表上，按一下 [**儲存**_table_name_]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-clustered-index"></a>若要建立叢集索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Create a new table with three columns.  
    CREATE TABLE dbo.TestTable  
        (TestCol1 int NOT NULL,  
         TestCol2 nchar(10) NULL,  
         TestCol3 nvarchar(50) NULL);  
    GO  
    -- Create a clustered index called IX_TestTable_TestCol1  
    -- on the dbo.TestTable table using the TestCol1 column.  
    CREATE CLUSTERED INDEX IX_TestTable_TestCol1   
        ON dbo.TestTable (TestCol1);   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [建立主索引鍵](../tables/create-primary-keys.md)   
 [建立唯一的條件約束](../tables/create-unique-constraints.md)  
  
  
