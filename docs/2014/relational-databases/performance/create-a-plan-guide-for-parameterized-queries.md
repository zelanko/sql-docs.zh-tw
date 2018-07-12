---
title: 建立參數化查詢的計畫指南 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameterized queries, plan guides for
- plan guides [SQL Server], parameterized queries
ms.assetid: b532ae16-66e7-4641-9bc8-b0d805853477
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: dfdacfb9764e607737946ccb8dc72d330f6b11a3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430971"
---
# <a name="create-a-plan-guide-for-parameterized-queries"></a>建立參數化查詢的計畫指南
  TEMPLATE 計畫指南可搭配參數化為指定形式的獨立查詢。  
  
 下列範例會建立與參數化為特定格式的任何查詢相符的計畫指南，並導引 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以強制執行查詢的參數化作業。 下列兩項查詢在語法上相同，不同的只是兩者的常數值。  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 以下是參數化格式查詢的計畫指南：  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 在前一個範例中， `@stmt` 參數的值是參數化格式的查詢。 取得這個值以便於 sp_create_plan_guide 中使用的唯一可靠方法，是利用 [sp_get_query_template](/sql/relational-databases/system-stored-procedures/sp-get-query-template-transact-sql) 系統預存程序。 下列指令碼可以用來取得參數化查詢，之後再建立參數化查詢的計畫指南。  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  傳送到 `@stmt` 之 `sp_get_query_template` 參數中的常數常值，可能會影響針對取代常值的參數所選擇的資料類型。 這會影響計畫指南的比對作業。 您可能需要建立一份以上的計畫指南，來處理不同的參數值範圍。  
  
 您也可以同時使用 TEMPLATE 計畫指南與 SQL 計畫指南。 例如，您可以建立 TEMPLATE 計畫指南以確定參數化查詢類別。 接著就可以在該查詢的參數化形式上建立 SQL 計畫指南。  
  
  
