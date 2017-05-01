---
title: "修改外部索引鍵關聯性 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:65538
- vdt.ppg.relationships
helpviewer_keywords:
- foreign keys [SQL Server], modifying
- modifying foreign keys
ms.assetid: 0c9ca80d-d79b-44c4-a21e-0fce39c398ec
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d938937ff7d4009ec874ebc9bbd33b2e87960def
ms.lasthandoff: 04/11/2017

---
# <a name="modify-foreign-key-relationships"></a>修改外部索引鍵關聯性
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中修改關聯性的外部索引鍵端。 修改資料表的外部索引鍵，會變更與主索引鍵資料表中之資料行相關的資料行。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法修改外部索引鍵：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 新的外部索引鍵資料行必須符合其相關主要索引鍵資料行的資料類型和大小，但是例外如下：  
  
-   **char** 資料行或 **sysname** 資料行可以與 **varchar** 資料行相關聯。  
  
-   **binary** 資料行可以與 **varbinary** 資料行相關聯。  
  
-   別名資料類型可以與其基底類型相關聯。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-foreign-key"></a>若要修改外部索引鍵  
  
1.  在 **[物件總管]**中，展開含有外部索引鍵的資料表，然後展開 **[索引鍵]**。  
  
2.  以滑鼠右鍵按一下您要修改的外部索引鍵，然後選取 [修改]。  
  
3.  在 **[外部索引鍵關聯性]** 對話方塊中，您可以進行下列修改。  
  
     **選取的關聯性**  
     列出現有的關聯性。 選取關聯性，在右邊方格中顯示其屬性。 如果清單是空的，表示此資料表沒有定義關聯性。  
  
     **加入**  
     建立新的關聯性。 [ **資料表及資料行規格** ] 必須在關聯性生效之前設定。  
  
     **Delete**  
     在 [選取的關聯性] 清單中刪除選取的關聯性。 若要刪除加入的關聯性，請使用此按鈕移除該關聯性。  
  
     **一般類別目錄**  
     展開以顯示 [檢查建立或重新啟用時的現有資料] 以及 [資料表及資料行規格]。  
  
     **檢查建立或重新啟用時的現有資料**  
     在建立或重新啟用條件約束之前，依照條件約束驗證資料表中所有現有的資料。  
  
     **資料表及資料行規格分類**  
     展開以顯示哪些資料表的哪些資料行，在關聯性中做為外部索引鍵和主要 (或唯一) 索引鍵。 若要編輯或定義這些值，請按一下屬性欄位右邊的省略符號按鈕 (**…**)。  
  
     **外部索引鍵基底資料表**  
     顯示所選取的關聯性中，哪些資料表包含有做為外部索引鍵的資料行。  
  
     **外部索引鍵資料行**  
     顯示所選取的關聯性中，哪些資料行做為外部索引鍵。  
  
     **主/唯一索引鍵基底資料表**  
     顯示所選取的關聯性中，哪些資料表包含有做為主要 (或唯一) 索引鍵的資料行。  
  
     **主/唯一索引鍵資料行**  
     顯示所選取的關聯性中，哪些資料行做為主要 (或唯一) 索引鍵。  
  
     **識別類別目錄**  
     展開以顯示 [名稱] 和 [描述] 的屬性欄位。  
  
     **名稱**  
     顯示關聯性的名稱。 在建立新的關聯性時，會根據 [ **資料表設計工具**] 作用中視窗的資料表，給予預設的名稱。 您可以隨時變更名稱。  
  
     **描述**  
     描述關聯性。 若要撰寫更詳細的描述，請按一下 [描述]，然後按一下屬性欄位右邊的省略符號 **(...)**。 如此便可提供較大的區域以寫入文字。  
  
     **資料表設計工具類別目錄**  
     展開以顯示 [檢查建立或重新啟用時的現有資料] 和 [強制複寫] 的資訊。  
  
     **強制複寫**  
     指示當複寫代理程式在此資料表上執行插入、更新或刪除時，是否要強制使用條件約束。  
  
     **強制使用外部索引鍵條件約束**  
     指定變更關聯性中的資料行資料時，如果變更會破壞外部索引鍵關聯性的完整性，是否允許執行。 如果不允許這樣的變更，請選擇 [ **是** ]，如果允許，請選擇 [ **否** ]。  
  
     **INSERT 和 UPDATE 規格分類**  
     展開以顯示關聯性之 [刪除規則] 和 [更新規則] 的資訊。  
  
     **刪除規則**  
     指定當使用者嘗試刪除與外部索引鍵關聯性相關的資料列時，應該採取什麼動作：  
  
    -   **沒有動作** ：錯誤訊息會告知使用者不允許執行刪除，並且會回復 DELETE 命令。  
  
    -   **串聯** ：刪除包含與外部索引鍵關聯性相關之資料的所有資料列。 如果資料表要包含在使用邏輯記錄的合併式發行集中，請勿指定 CASCADE。  
  
    -   **設為 Null** ：如果資料表的所有外部索引鍵資料行都可以接受 null 值，就可以將值設為 null。  
  
    -   **設為預設值** ：如果資料表的所有外部索引鍵資料行都具有為其所定義的預設值，就可以將值設為資料行所定義的預設值。  
  
     **更新規則**  
     指定當使用者嘗試更新與外部索引鍵關聯性相關的資料列時，應該採取什麼動作：  
  
    -   **沒有動作** ：錯誤訊息會告知使用者不允許執行更新，並且會還原 UPDATE 命令。  
  
    -   **串聯** ：更新包含與外部索引鍵關聯性相關之資料的所有資料列。 如果資料表要包含在使用邏輯記錄的合併式發行集中，請勿指定 CASCADE。  
  
    -   **設為 Null** ：如果資料表的所有外部索引鍵資料行都可以接受 null 值，就可以將值設為 null。  
  
    -   **設為預設值** ：如果資料表的所有外部索引鍵資料行都具有為其所定義的預設值，就可以將值設為資料行所定義的預設值。  
  
4.  在 [檔案]  功能表上，按一下 [儲存] *table name*。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要修改外部索引鍵**  
  
 若要使用 Transact-SQL 修改 FOREIGN KEY 條件約束，您必須先刪除現有的 FOREIGN KEY 條件約束，然後使用新的定義來重新建立。 如需相關資訊，請參閱 [Delete Foreign Key Relationships](../../relational-databases/tables/delete-foreign-key-relationships.md) 及 [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md)。  
  
###  <a name="TsqlExample"></a>  
