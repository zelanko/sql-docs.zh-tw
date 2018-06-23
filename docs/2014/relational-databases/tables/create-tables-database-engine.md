---
title: 建立資料表 (Database Engine) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- table creation [SQL Server], Visual Database Tools
ms.assetid: 6f7c6ac5-e6d3-4dca-831e-b28442ba535b
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e4a25a40c2af9d5c5d636a8576ee487135009a24
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036525"
---
# <a name="create-tables-database-engine"></a>建立資料表 (Database Engine)
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立新資料表、為資料表命名，並將它加入至現有資料庫。  
  
> [!NOTE]  
>  如果您連接到 SQL Azure 資料庫，新的資料表選項將會啟動建立資料表範本指令碼。 請編輯參數，然後執行指令碼來建立新的資料表。 如需詳細資訊，請參閱＜ [SQL Azure 概觀](http://go.microsoft.com/fwlink/?LinkId=163948)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要建立資料表時，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料庫的 CREATE TABLE 權限以及用以建立資料表之結構描述的 ALTER 權限。  
  
 如果將 CREATE TABLE 陳述式中的任何資料行定義成 CLR 使用者定義型別，就需要類型的擁有權或它的 REFERENCES 權限。  
  
 如果 CREATE TABLE 陳述式中的任何資料行有相關聯的 XML 結構描述集合，就需要 XML 結構描述集合的擁有權或它的 REFERENCES 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-table-with-table-designer"></a>若要使用資料表設計工具建立資料表  
  
1.  在 **[物件總管]**，連接至包含要修改的資料庫的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。  
  
2.  在 **[物件總管]** 中，展開 **[資料庫]** 節點，然後展開將包含新資料表的資料庫。  
  
3.  在物件總管中，以滑鼠右鍵按一下資料庫的 [資料表] 節點，然後按一下 [新增資料表]。  
  
4.  輸入資料行名稱，選擇資料類型，然後選擇是否允許讓每個資料行都是 null，如下圖所示。  
  
     ![AddColumnsinTableDesigner](../../database-engine/media/addcolumnsintabledesigner.gif "AddColumnsinTableDesigner")  
  
5.  若要指定資料行的其他屬性，例如識別或計算資料行值，請按一下資料行，然後在資料行屬性索引標籤中選擇適當的屬性。 如需資料行屬性的詳細資訊，請參閱[資料表資料行屬性 &#40;SQL Server Management Studio&#41;](table-column-properties-sql-server-management-studio.md)。  
  
6.  若要指定資料行做為主索引鍵，請以滑鼠右鍵按一下資料行並選取 [設定主索引鍵]。 如需詳細資訊，請參閱 [Create Primary Keys](../tables/create-primary-keys.md)。  
  
7.  若要建立外部索引鍵關聯性、檢查條件約束或索引，請在 [資料表設計工具] 窗格中按一下滑鼠右鍵並選取清單中的物件，如下圖所示。  
  
     ![AddTableObjects](../../database-engine/media/addtableobjects.gif "AddTableObjects")  
  
     如需有關這些物件的詳細資訊，請參閱＜ [Create Foreign Key Relationships](../tables/create-foreign-key-relationships.md)＞、＜ [Create Check Constraints](../tables/create-check-constraints.md) ＞和＜ [Indexes](../indexes/indexes.md)＞。  
  
8.  依預設，此資料表包含在 **dbo** 結構描述中。 若要為資料表指定不同的結構描述，請在 [資料表設計工具] 窗格中按一下滑鼠右鍵並選取 [屬性]，如下圖所示。 從 [結構描述] 下拉式清單中選取適當的結構描述。  
  
     ![Specifyatableschema](../../database-engine/media/specifyatableschema.gif "Specifyatableschema")  
  
     如需有關結構描述的詳細資訊，請參閱＜ [Create a Database Schema](../security/authentication-access/create-a-database-schema.md)＞。  
  
9. 從 [檔案]  功能表中，選擇 [儲存]  *table name*。  
  
10. 在 **[選擇名稱]** 對話方塊中，輸入資料表的名稱，然後按一下 **[確定]**。  
  
11. 若要檢視新的資料表，在 **[物件總管]**，展開 **[資料表]** 節點並按 **F5** 重新整理物件清單。 新的資料表就會在資料表清單中顯示。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-table-in-the-query-editor"></a>若要在查詢編輯器中建立資料表  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    CREATE TABLE dbo.PurchaseOrderDetail  
    (  
        PurchaseOrderID int NOT NULL  
        ,LineNumber smallint NOT NULL  
        ,ProductID int NULL  
        ,UnitPrice money NULL  
        ,OrderQty smallint NULL  
        ,ReceivedQty float NULL  
        ,RejectedQty float NULL  
        ,DueDate datetime NULL  
    );  
    ```  
  
 如需更多範例，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)。  
  
  
