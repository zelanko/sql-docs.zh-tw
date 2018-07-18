---
title: 建立非叢集索引 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- index creation [SQL Server], nonclustered indexes
- nonclustered indexes [SQL Server], creating
- nonclustered indexes [SQL Server], UNIQUE constraint
- indexes [SQL Server], nonclustered
- nonclustered indexes [SQL Server], PRIMARY KEY constraint
ms.assetid: 9402029a-1227-46c4-93aa-c2122eb1b943
caps.latest.revision: 41
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7f0735f394e7814e4916e79c88124c0a199dfeba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32939903"
---
# <a name="create-nonclustered-indexes"></a>建立非叢集索引
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立非叢集索引。 非叢集索引是與資料表中所儲存之資料不同的索引結構，可重新排序一個或多個選取的資料行。 非叢集索引經常可協助您以比搜尋基礎資料表更快的速度找到資料；查詢的結果有時會完全來自非叢集索引中的資料，或是非叢集索引可能會將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 指向基礎資料表中的資料列。 一般而言，建立非叢集索引是為了改善叢集索引未涵蓋但經常使用之查詢的效能，或尋找沒有叢集索引之資料表中的資料列 (稱為堆積)。 您可以在資料表或索引檢視表上建立多個非叢集索引。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Implementations"></a> 一般實作  
 非叢集索引的實作方法如下：  
  
-   **UNIQUE 條件約束**  
  
     當您建立 UNIQUE 條件約束時，依預設會建立唯一的非叢集索引，以強制 UNIQUE 條件約束。 若資料表上還沒有叢集索引，您可以指定唯一叢集索引。 如需詳細資訊，請參閱 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)。  
  
-   **獨立於條件限制之外的索引**  
  
     依預設，若是未指定叢集索引，則會建立非叢集索引。 每個資料表可建立的最大非叢集索引數目是 999 個。 這包含 PRIMARY KEY 或 UNIQUE 條件約束所建立的任何索引，但不包含 XML 索引。  
  
-   **索引檢視上的非叢集索引**  
  
     在檢視上建立唯一的叢集索引後，就可以建立非叢集索引。 如需詳細資訊，請參閱 [建立索引檢視表](../../relational-databases/views/create-indexed-views.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-nonclustered-index-by-using-the-table-designer"></a>若要使用資料表設計工具建立非叢集索引  
  
1.  在 [物件總管] 中，展開包含您要建立非叢集索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  以滑鼠右鍵按一下要建立非叢集索引的資料表，然後選取 [設計]。  
  
4.  在 [資料表設計工具] 功能表上，按一下 [索引/索引鍵]。  
  
5.  在 [索引/索引鍵] 對話方塊中，按一下 [加入]。  
  
6.  從 [選取的主索引鍵/唯一索引鍵或索引] 文字方塊中選取新索引。  
  
7.  在方格中，選取 [建立成 CLUSTERED]，然後從屬性右邊的下拉式清單中選擇 [否]。  
  
8.  按一下 [ **關閉**]。  
  
9. 在 [檔案] 功能表上，按一下 [儲存 <資料表名稱>]。  
  
#### <a name="to-create-a-nonclustered-index-by-using-object-explorer"></a>若要使用物件總管建立非叢集索引  
  
1.  在 [物件總管] 中，展開包含您要建立非叢集索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  展開您要建立非叢集索引的資料表。  
  
4.  以滑鼠右鍵按一下 [索引] 資料夾，指向 [新增索引]，然後選取 [非叢集索引…]。  
  
5.  在 **[新增索引]** 對話方塊，於 **[一般]** 頁面上的 **[索引名稱]** 方塊中輸入新索引的名稱。  
  
6.  按一下 **[索引鍵資料行]** 底下的 **[加入]**。  
  
7.  在 [從 <資料表名稱> 選取資料行] 對話方塊中，選取要新增至非叢集索引之一或多個資料表資料行的核取方塊。  
  
8.  按一下 [確定] 。  
  
9. 在 **[新增索引]** 對話方塊中，按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-nonclustered-index-on-a-table"></a>若要在資料表上建立非叢集索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named IX_ProductVendor_VendorID and delete it if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
                WHERE name = N'IX_ProductVendor_VendorID')   
        DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;   
    GO  
    -- Create a nonclustered index called IX_ProductVendor_VendorID   
    -- on the Purchasing.ProductVendor table using the BusinessEntityID column.   
    CREATE NONCLUSTERED INDEX IX_ProductVendor_VendorID   
        ON Purchasing.ProductVendor (BusinessEntityID);   
    GO  
    ```  
  
## <a name="related-content"></a>相關內容  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
[SQL Server 索引設計指南](../../relational-databases/sql-server-index-design-guide.md) 
