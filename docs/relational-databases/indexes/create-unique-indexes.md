---
title: 建立唯一索引 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- unique indexes
- designing indexes [SQL Server], unique
- clustered indexes, unique
- indexes [SQL Server], unique
- nonclustered indexes [SQL Server], unique
- unique indexes, design guidelines
ms.assetid: 56b5982e-cb94-46c0-8fbb-772fc275354a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7129c5feb6bc23a7e72dddfa70a10d4d2bc0811c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67898599"
---
# <a name="create-unique-indexes"></a>建立唯一索引
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]的資料表建立唯一索引。 唯一索引可保證索引鍵不包含重複值，因此資料表中的每一個資料列在某方面來說是唯一的。 建立 UNIQUE 條件約束與建立獨立於條件約束之外的唯一索引，兩者並無明顯差異。 資料驗證的方式相同，而且查詢最佳化工具不會區分由條件約束建立或由手動建立的唯一索引。 不過，在資料行上建立 UNIQUE 條件約束，會使索引目標更明確。 如需有關 UNIQUE 條件約束的詳細資訊，請參閱＜ [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)＞。  
  
 當您建立唯一的索引時，可以設定忽略重複之索引鍵的選項。 如果此選項設定為 [是]  ，且您嘗試透過加入影響多個資料列的資料來建立重複的索引鍵 (使用 INSERT 陳述式)，則不會加入包含重複索引鍵的資料列。 如果此選項設定為 [ **否**]，則整個插入作業會失敗，且所有資料都會回復。  
  
> [!NOTE]  
>  如果一個以上的資料列中的某單一資料行為 NULL，您將無法建立該單一資料行的唯一索引。 同樣地，如果一個以上的資料列中的一組資料行全為 NULL 的話，您將無法在該組資料行上建立唯一索引。 基於索引目的，這些會被視為重複的值。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [唯一索引的優點](#Benefits)  
  
     [一般實作](#Implementations)  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法在資料表上建立唯一索引：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Benefits"></a> 唯一索引的優點  
  
-   多重資料行唯一索引可保證索引鍵的每一個值組合都是唯一的。 例如，若在 **LastName**、 **FirstName**和 **MiddleName** 資料行的組合上建立唯一索引，則該資料表中不得有兩個資料列具有這些資料行的相同值組合。  
  
-   假設每個資料行中的資料是唯一的，您就可以在同一個資料表上建立一個唯一的叢集索引和多個唯一的非叢集索引。  
  
-   唯一索引可確保所定義資料行的資料完整性。  
  
-   唯一索引提供額外資訊給查詢最佳化工具，有助於產生更有效率的執行計畫。  
  
###  <a name="Implementations"></a> 一般實作  
 唯一索引的實作方式如下：  
  
-   **PRIMARY KEY 或 UNIQUE 條件約束**  
  
     建立 PRIMARY KEY 條件約束時，若資料表上沒有存在叢集索引，而且您未指定唯一的非叢集索引，則資料行上會自動建立唯一的叢集索引。 主索引鍵資料行不允許 NULL 值。  
  
     當您建立 UNIQUE 條件約束時，依預設會建立唯一的非叢集索引，以強制 UNIQUE 條件約束。 若資料表上還沒有叢集索引，您可以指定唯一叢集索引。  
  
     如需相關資訊，請參閱 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 及 [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md)。  
  
-   **獨立於條件限制之外的索引**  
  
     一個資料表上可定義多個唯一的非叢集索引。  
  
     如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)。  
  
-   **索引檢視表**  
  
     若要建立索引檢視，您必須在一個或多個檢視資料行上定義唯一的叢集索引。 將會執行檢視，而結果集會以資料表資料儲存在叢集索引中的相同方式，儲存在索引的分葉層級。 如需詳細資訊，請參閱 [建立索引檢視表](../../relational-databases/views/create-indexed-views.md)。  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果資料中已存在重複的索引鍵值，則無法建立唯一索引、UNIQUE 條件約束或 PRIMARY KEY 條件約束。  
  
-   唯一非叢集索引可有內含的非索引鍵之索引資料行。 如需詳細資訊，請參閱 [建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-unique-index-by-using-the-table-designer"></a>若要使用資料表設計工具建立唯一索引  
  
1.  在 [物件總管] 中，展開包含您要建立唯一索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  以滑鼠右鍵按一下要建立唯一索引的資料表，然後選取 [設計]  。  
  
4.  在 [資料表設計工具]  功能表中，選取 [索引/索引鍵]  。  
  
5.  在 [索引/索引鍵]  對話方塊中，按一下 [加入]  。  
  
6.  從 [選取的主索引鍵/唯一索引鍵或索引]  文字方塊中選取新索引。  
  
7.  在主要方格的 [(一般)]  底下，選取 [類型]  ，然後從清單中選擇 [索引]  。  
  
8.  選取 [資料行]  ，然後按一下省略符號 **(...)** 。  
  
9. 在 **[索引資料行]** 對話方塊中的 **[資料行名稱]** 底下，選取要進行索引的資料行。 您最多可以選取 16 個資料行。 為了獲得最佳效能，每個索引最好只選取一或兩個資料行。 針對每個選取的資料行，指示索引是要以遞增或遞減順序排列此資料行的值。  
  
10. 選取索引的所有資料行時，請按一下 **[確定]** 。  
  
11. 在方格的 [(一般)]  底下，選取 [是唯一的]  ，然後從清單中選擇 [是]  。  
  
12. 選擇性：在主要方格中的 **[資料表設計工具]** 底下，選取 **[忽略重複的索引鍵]** ，然後從清單選擇 **[是]** 。 如果您要忽略會在唯一的索引中建立重複索引鍵的加入資料嘗試，請執行這個動作。  
  
13. 按一下 [關閉]  。  
  
14. 在 [檔案]  功能表上，按一下 [儲存 **table**name _]\__ 。  
  
#### <a name="create-a-unique-index-by-using-object-explorer"></a>使用物件總管建立唯一索引  
  
1.  在 [物件總管] 中，展開包含您要建立唯一索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  展開您要建立唯一索引的資料表。  
  
4.  以滑鼠右鍵按一下 [索引]  資料夾，指向 [新增索引]  ，然後選取 [非叢集索引…]  。  
  
5.  在 **[新增索引]** 對話方塊，於 **[一般]** 頁面上的 **[索引名稱]** 方塊中輸入新索引的名稱。  
  
6.  選取 **[唯一]** 核取方塊。  
  
7.  按一下 [索引鍵資料行]  下的 [新增...]  。  
  
8.  在 [從 **table**name _選取資料行]\__ 對話方塊中，選取要新增至唯一索引之一或多個資料表資料行的一或多個核取方塊。  
  
9. 按一下 [確定]  。  
  
10. 在 **[新增索引]** 對話方塊中，按一下 **[確定]** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-unique-index-on-a-table"></a>在資料表上建立唯一索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named AK_UnitMeasure_Name and delete it if found  
    IF EXISTS (SELECT name from sys.indexes  
               WHERE name = N'AK_UnitMeasure_Name')   
       DROP INDEX AK_UnitMeasure_Name ON Production.UnitMeasure;   
    GO  
    -- Create a unique index called AK_UnitMeasure_Name  
    -- on the Production.UnitMeasure table using the Name column.  
    CREATE UNIQUE INDEX AK_UnitMeasure_Name   
       ON Production.UnitMeasure (Name);   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)。  
  
  
