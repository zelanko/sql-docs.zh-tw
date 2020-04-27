---
title: 建立使用者定義資料類型別名 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.userdefineddatatype.general.f1
- sql12.swb.new.datatype.properties.general.f1
helpviewer_keywords:
- alias data types [SQL Server], creating
ms.assetid: b1dd8413-0cd0-411b-a79b-1bb043ccc62d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b073e6025bc1483db2482a03d525b758d39efea4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62917442"
---
# <a name="create-a-user-defined-data-type-alias"></a>建立使用者定義資料類型別名
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立新的使用者定義資料類型別名。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法建立使用者定義資料類型別名：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   使用者定義資料類型別名的名稱必須符合識別碼的規則。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要目前資料庫的 CREATE TYPE 權限，以及 *schema_name*的 ALTER 權限。 如果未指定 *schema_name* ，則套用用來判斷目前使用者之結構描述的預設名稱解析規則。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-user-defined-data-type"></a>若要建立使用者自訂的資料類型  
  
1.  在物件總管中，依序展開 [資料庫]  、某個資料庫、[可程式性]  和 [類型]  ，並以滑鼠右鍵按一下 [使用者定義資料類型]  ，然後按一下 [新增使用者定義資料類型]  。  
  
     **允許 NULL**  
     指定使用者定義資料類型是否可接受 NULL 值。 無法編輯現有使用者定義資料類型的 Null 屬性。  
  
     **Data type**  
     從清單方塊中選取基底資料類型。 這個清單方塊會顯示除了 `geography`、`geometry`、`hierarchyid`、`sysname`、`timestamp` 和 `xml` 資料類型以外的所有資料類型。 無法編輯現有使用者定義資料類型的資料類型。  
  
     **預設值**  
     選擇性地選取繫結到使用者定義資料類型別名的規則或預設值。  
  
     **長度/有效位數**  
     顯示適用之資料類型的長度或有效位數。 [長度]  適用於字元為主的使用者定義資料類型；[有效位數]  只適用於數值為主的使用者定義資料類型。 標籤會根據稍早選取的資料類型而變更。 如果選取之資料類型的長度或有效位數是固定的，則無法編輯此方塊。  
  
     `nvarchar(max)`、`varchar(max)` 或 `varbinary(max)` 資料類型不會顯示長度。  
  
     **名稱**  
     如果您正在建立新的使用者定義資料類型別名，請輸入跨資料庫使用以代表使用者定義資料類型的唯一名稱。 字元數目上限必須符合系統`sysname`資料類型。 無法編輯現有的使用者定義資料類型別名的名稱。  
  
     **規則**  
     選擇性地選取繫結到使用者定義資料類型別名的規則。  
  
     **調整**  
     指定小數點右方的小數位數上限。  
  
     **結構描述**  
     從目前使用者可用的所有結構描述清單中選取結構描述。 預設選取項目是目前使用者的預設結構描述。  
  
     **Storage**  
     顯示使用者定義資料類型別名的儲存體大小上限。 儲存體大小上限會根據有效位數而不同。  
  
    |||  
    |-|-|  
    |1 - 9|5|  
    |10 - 19|9|  
    |20 - 28|13|  
    |29 - 38|17|  
  
     針對`nchar`和`nvarchar`資料類型，儲存體值一律為 [**長度**] 值的兩倍。  
  
     `nvarchar(max)`、`varchar(max)` 或 `varbinary(max)` 資料類型不會顯示儲存體。  
  
2.  在 [新增使用者定義資料類型]  對話方塊的 [結構描述]  方塊中，輸入要擁有此資料類型別名的結構描述，或使用瀏覽按鈕來選取結構描述。  
  
3.  在 **[名稱]** 方塊中，輸入新資料類型別名的名稱。  
  
4.  在 **[資料類型]** 方塊中，選取將做為新資料類型別名基礎的資料類型。  
  
5.  依該資料類型的情況，完成 **[長度]** 、 **[有效位數]** 和 **[小數位數]** 方塊。  
  
6.  若新的資料類型別名可允許 NULL 值，請選取 **[允許 NULL]** 。  
  
7.  若您要將預設值或規則繫結至新的資料類型別名，請在 **[繫結]** 區域中，完成 **[預設值]** 或 **[規則]** 方塊。 您不能在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中建立預設值和規則。 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 [範本總管] 中有可供建立預設值和規則的範例程式碼。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-user-defined-data-type-alias"></a>若要建立使用者定義資料類型別名  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例根據系統提供的 `varchar` 資料類型建立資料類型別名。 `ssn` 資料類型別名用於保留 11 位數之社會保險號碼 (999-99-9999) 的資料行。 該資料行不能是 NULL。  
  
```sql  
CREATE TYPE ssn  
FROM varchar(11) NOT NULL ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫識別碼](database-identifiers.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql)  
  
  
