---
title: 檢視統計資料屬性 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.statistics.details.f1
helpviewer_keywords:
- viewing statistics properties
- statistics [SQL Server], viewing properties
ms.assetid: 0eaa2101-006e-4015-9979-3468b50e0aaa
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1fc876283635f3a3015efa957b90cf0d9d938386
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001049"
---
# <a name="view-statistics-properties"></a>檢視統計資料屬性
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中針對資料表或索引檢視表顯示目前的查詢最佳化統計資料。 統計資料物件包含標頭 (其中包含有關統計資料的中繼資料)、長條圖 (包含統計資料物件之第一個索引鍵資料行中的值分佈)，以及用來測量跨資料行關聯的密度向量。 如需長條圖和密度向量的詳細資訊，請參閱 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目檢視統計資料屬性：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 使用者必須擁有資料表，或者使用者必須是 **系統管理員** 固定伺服器角色、 **db_owner** 固定資料庫角色或 **db_ddladmin** 固定資料庫角色的成員，才能檢視統計資料物件。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-statistics-properties"></a>若要檢視統計資料屬性  
  
1.  在 **[物件總管]** 中，按一下加號展開要在其中建立新統計資料的資料庫。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要在其中檢視統計資料屬性的資料表。  
  
4.  按一下加號展開 **[統計資料]** 資料夾。  
  
5.  以滑鼠右鍵按一下要檢視其屬性的統計資料物件，然後選取 [屬性]  。  
  
6.  在 [統計資料屬性 - **statistics_name**]  對話方塊的 [選取頁面]  窗格中，選取 [詳細資料]  。  
  
     下列屬性會在 [統計資料屬性 - **statistics_name**]  對話方塊的 [詳細資料]  頁面中顯示。  
  
     **資料表名稱**  
     顯示統計資料所描述的資料表名稱。  
  
     **統計資料名稱**  
     顯示儲存統計資料的資料庫物件名稱。  
  
     **INDEXstatistics_name 的統計資料**  
     此文字方塊顯示從統計資料物件傳回的屬性。 屬性分為三個部分：統計資料標頭、密度向量和長條圖。  
  
     下列資訊描述結果集針對統計資料標頭所傳回的資料行。  
  
     **名稱**  
     統計資料物件的名稱。  
  
     **已更新**  
     上次更新統計資料的日期和時間。  
  
     **資料列**  
     上一次更新統計資料時位於資料表或索引檢視表中的資料列總數。 如果篩選了統計資料或是統計資料對應至篩選過的索引，此資料列數可能會少於資料表中的資料列數。  
  
     **取樣的資料列**  
     針對統計資料計算進行取樣的資料列總數。 如果取樣的資料列數 < 資料列數，顯示的長條圖和密度結果將會是根據取樣資料列數的預估值。  
  
     **步驟**  
     長條圖中的步驟數。 每一個步驟都會跨越某個範圍的資料行值，後面緊接著上限資料行值。 長條圖步驟會在統計資料中的第一個索引鍵資料行上定義。 步驟數的最大值為 200。  
  
     **密度**  
     針對統計資料物件第一個索引鍵資料行中的所有值，計算為 1 / 相異值  ，不包括長條圖界限值。 查詢最佳化工具不會使用這個密度值，而且會針對與 SQL Server 2008 之前版本之間的回溯相容性顯示。  
  
     **平均索引鍵長度**  
     針對統計資料物件中的所有索引鍵資料行計算之每個值的平均位元組數。  
  
     **String Index**  
     Yes 表示統計資料物件包含了字串摘要統計資料來改善使用 LIKE 運算子之查詢述詞的基數預估，例如 `WHERE ProductName LIKE '%Bike'`。 字串摘要統計資料會與長條圖分開儲存，而且會在具有 **char**、 **varchar**、 **nchar**、 **nvarchar**、 **varchar(max)** 、 **nvarchar(max)** 、 **text**或 **ntext**類型時於統計資料物件的第一個索引鍵資料行上建立。  
  
     **篩選運算式**  
     包含在統計資料物件中之資料表資料列子集的述詞。 NULL = 非篩選的統計資料。  
  
     **Unfiltered Rows**  
     套用篩選運算式之前，資料表中的資料列總數。 如果 Filter Expression 為 NULL，Unfiltered Rows 就會等於 Rows。  
  
     下列資訊描述結果集針對密度向量所傳回的資料行。  
  
     **所有密度**  
     密度是 1 / 相異值  。 結果會針對統計資料物件中資料行的每個前置詞來顯示密度，一個密度一個資料列。 相異值是每個資料列和每個資料行前置詞的資料行值相異清單。 例如，如果統計資料物件包含索引鍵資料行 (A, B, C)，結果就會報告每一個資料行前置詞中相異值清單的密度：(A)、(A,B) 和 (A, B, C)。 使用前置詞 (A, B, C) 時，這些清單的每一個都會是相異值清單：(3, 5, 6)、(4, 4, 6)、(4, 5, 6)、(4, 5, 7)。 使用前置詞 (A, B) 時，相同的資料行值都會有這些相異值清單：(3, 5)、(4, 4) 和 (4, 5)。  
  
     **平均長度**  
     平均長度 (以位元組為單位)，用來儲存資料行前置詞的資料行值清單。 例如，如果清單 (3, 5, 6) 中的每一個值都需要 4 位元組，長度就是 12 位元組。  
  
     **資料行**  
     在前置詞中顯示 All density 和 Average length 的資料行名稱。  
  
     下列資訊描述結果集針對長條圖所傳回的資料行。  
  
     **RANGE_HI_KEY**  
     長條圖步驟的上限資料行值。 此資料行值也稱為索引鍵值。  
  
     **RANGE_ROWS**  
     資料行值在長條圖步驟內的預估資料列數，不包括上限。  
  
     **EQ_ROWS**  
     資料行值等於長條圖步驟之上限的預估資料列數。  
  
     **DISTINCT_RANGE_ROWS**  
     在長條圖步驟內具有相異資料行值的預估資料列數，不包括上限。  
  
     **AVG_RANGE_ROWS**  
     在長條圖步驟內具有重複資料行值的平均資料列數，上限不包括在內 (RANGE_ROWS / DISTINCT_RANGE_ROWS for DISTINCT_RANGE_ROWS > 0)。  
  
7.  按一下 [確定]  。  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-statistics-properties"></a>若要檢視統計資料屬性  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example displays all statistics information for the AK_Address_rowguid index of the Person.Address table.   
    DBCC SHOW_STATISTICS ("Person.Address", AK_Address_rowguid);   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)。  
  
#### <a name="to-find-all-of-the-statistics-on-a-table-or-view"></a>若要尋找資料表或檢視表的所有統計資料  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Gets the following information: name and ID of the statistics, whether the statistics were created automatically or by the user, whether the statistics were created with the NORECOMPUTE option, and whether the statistics have a filter and, if so, what that filter is.  
    */  
    SELECT name AS statistics_name  
        ,stats_id  
        ,auto_created  
        ,user_created  
        ,no_recompute  
        ,has_filter  
        ,filter_definition  
    -- using the sys.stats catalog view  
    FROM sys.stats  
    -- for the Sales.SpecialOffer table  
    WHERE object_id = OBJECT_ID('Sales.SpecialOffer');  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)。  
  
  
