---
title: 執行使用者定義函式 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7e9c170a187fc3ccf28301a2ee1c9ee7b626169f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196438"
---
# <a name="execute-user-defined-functions"></a>執行使用者定義函數
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中執行使用者定義的函數。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要執行使用者定義函數，使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 在 Transact-SQL 中，您可以使用 *value* 或 @*parameter_name*=*value*來提供參數。 來提供參數。參數不是交易的一部分；因此，如果交易中的參數變更之後再回復，參數值並不會還原為之前的值。 傳回呼叫端的值一定是模組傳回時的值。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 執行 EXECUTE 陳述式不需要任何權限。 不過，您必須對 EXECUTE 字串內所參考的安全性實體具備權限。 例如，如果字串包含 INSERT 陳述式，EXECUTE 陳述式的呼叫端就必須有目標資料表的 INSERT 權限。 遇到 EXECUTE 陳述式時會檢查權限，即使模組內包含 EXECUTE 陳述式也一樣。 如需詳細資訊，請參閱[EXECUTE &#40;transact-sql&#41;](/sql/t-sql/language-elements/execute-transact-sql)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-execute-a-user-defined-function"></a>若要執行使用者定義函數  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Declares a variable and sets it to zero.  
    -- This variable is used to return the results of the function.  
    DECLARE @ret nvarchar(15)= NULL;   
  
    -- Executes the dbo.ufnGetSalesOrderStatusText function.  
    --The function requires a value for one parameter, @Status.   
    EXEC @ret = dbo.ufnGetSalesOrderStatusText @Status= 5;   
    --Returns the result in the message tab.  
    PRINT @ret;  
    ```  
  
 如需詳細資訊，請參閱 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)。  
  
  
