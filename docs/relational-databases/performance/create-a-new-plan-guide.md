---
title: 建立新的計畫指南 | Microsoft 文件
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL 來建立計畫指南。 計畫指南會將固定查詢計畫及查詢提示套用至查詢。
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.designer.newplanguide.f1
helpviewer_keywords:
- creating plan guides
- plan guides [SQL Server]. creating
ms.assetid: e1ad78bb-4857-40ea-a0c6-dcf5c28aef2f
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: b8f96167fff7c5d36209d43eedbbd53bc1daffee
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505322"
---
# <a name="create-a-new-plan-guide"></a>建立新的計畫指南
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
計畫指南是將查詢提示或固定的查詢計畫附加至查詢，以影響查詢的最佳化。 在計劃指南中，指定您要最佳化的陳述式或包含您想要使用之查詢提示的 OPTION 子句， 或者是您想要用來將查詢進行最佳化的特定查詢計劃。 在執行查詢的時候，查詢最佳化工具會比對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式與計畫指南，在執行階段將 OPTION 子句附加至查詢，或是使用特定的查詢計畫。  

計劃指南會將固定查詢計劃及/或查詢提示套用至查詢。
  
##  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
-   sp_create_plan_guide 的引數必須依照顯示順序提供。 當您提供 **sp_create_plan_guide** 的參數值時，必須明確指定所有的參數名稱，或是完全不指定。 例如，若指定了 **@name =** ，您也必須指定 **@stmt =** 、 **@type =** 等等。 同樣地，如果省略 **@name =** ，而只提供參數值，您也必須省略其餘參數名稱，只提供它們的值。 引數名稱僅供描述用途，以協助您了解語法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會驗證指定的參數名稱是否與使用該名稱之位置中的參數名稱相符。  
  
-   您可以針對相同的查詢和批次或模組，建立一個以上的 OBJECT 或 SQL 計畫指南。 但是，在任何指定的時間內，只能啟用一個計畫指南。  
  
-   若 @module_or_batch 值參考的預存程序、函數或 DML 觸發程序指定了 WITH ENCRYPTION 子句或是暫時項目，您就不能為這個值建立 OBJECT 類型的計畫指南。  
  
-   試圖卸除或修改計畫指南所參考的函數、預存程序或 DML 觸發程序，不論是已啟用或已停用，都會造成錯誤。 嘗試卸除定義了觸發程序且被計畫指南參考的資料表也會造成錯誤。  

##  <a name="permissions"></a><a name="Permissions"></a> 權限  
 若要建立類型為 OBJECT 的計劃指南，您需要所參考物件的 ALTER 權限。 若要建立類型為 SQL 或 TEMPLATE 的計劃指南，您需要目前資料庫的 ALTER 權限。  
  
##  <a name="create-a-plan-guide-using-ssms"></a><a name="SSMSProcedure"></a> 使用 SSMS 建立計劃指南  
1.  按一下加號，展開您要在其中建立計畫指南的資料庫，然後按一下加號展開 **[可程式性]** 資料夾。  
  
2.  以滑鼠右鍵按一下 [計畫指南] 資料夾，然後選取 [新增計畫指南…]。![select_plan_guide](../../relational-databases/performance/media/select-plan-guide.png)
  
3.  在 **[新增維護計畫]** 對話方塊中的 **[名稱]** 方塊，輸入計畫指南的名稱。  
  
4.  在 **[陳述式]** 方塊中，輸入對照套用計畫指南的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
5.  在 **[範圍類型]** 清單中，選取在其中顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的實體類型。 這會指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式要與計畫指南比對相符的內容。 可能的值是 **OBJECT**、 **SQL**，以及 **TEMPLATE**。  
  
6.  在 **[範圍批次]** 方塊中，輸入在其中顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的批次文字。 批次文字不能包含 `USE`*database* 陳述式。 **[範圍批次]** 方塊只在 **[SQL]** 選定為範圍類型時才可供使用。 如果 SQL 是範圍類型，但未在 [範圍批次] 方塊中輸入任何內容時，批次文字的值會設為與 **[陳述式]** 方塊中的值相同。  
  
7.  在 **[範圍結構描述名稱]** 清單中，輸入包含了該物件的結構描述名稱。 **[範圍結構描述名稱]** 方塊只在 **[物件]** 選定為範圍類型時才可供使用。  
  
8.  在 [範圍物件名稱] 方塊中，輸入顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序名稱、使用者定義純量函數名稱、多重陳述式資料表值函數名稱或 DML 觸發程序名稱。 **[範圍物件名稱]** 方塊只在 **[物件]** 選定為範圍類型時才可供使用。  
  
9. 在 **[參數]** 方塊中，輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中內嵌的所有參數的參數名稱與資料類型。  
  
   只有在下列兩者之一為真時，才套用參數：  
  
   -   範圍類型為 **SQL** 或 **TEMPLATE**。 如果是 **TEMPLATE**，參數必須不是 NULL。  
  
   -   [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式是使用已指定參數值的 sp_executesql 提交，或是在將它參數化之後，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部進行提交。  
  
10. 在 **[提示]** 方塊中，輸入套用到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的查詢提示或查詢計畫。 如需指定一或多個查詢提示，請輸入有效的 OPTION 子句。  
  
11. 按一下 [確定]。  

![plan_guide](../../relational-databases/performance/media/plan-guide.png)  

##  <a name="create-a-plan-guide-using-t-sql"></a><a name="TsqlProcedure"></a> 使用 T-SQL 建立計劃指南  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
  
    ```  

如需詳細資訊，請參閱 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)。  

  
