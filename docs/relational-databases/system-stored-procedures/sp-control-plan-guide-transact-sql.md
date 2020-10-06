---
description: sp_control_plan_guide (Transact-SQL)
title: sp_control_plan_guide (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_control_plan_guide
- sp_control_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_plan_guide
ms.assetid: c96d43d5-6507-4d66-b3f5-f44c0617cb5c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5a66806fa3c4865da7486a7ada3c46a9691be6d7
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753900"
---
# <a name="sp_control_plan_guide-transact-sql"></a>sp_control_plan_guide (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  卸除、啟用或停用計畫指南。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_control_plan_guide [ @operation = ] N'<control_option>'  
  [ , [ @name = ] N'plan_guide_name' ]  
  
<control_option>::=  
{   
    DROP   
  | DROP ALL  
  | DISABLE  
  | DISABLE ALL  
  | ENABLE   
  | ENABLE ALL  
}  
```  
  
## <a name="arguments"></a>引數  
 **N '** _plan_guide_name_ **'**  
 指定要卸除、啟用或停用的計畫指南。 *plan_guide_name* 會解析為目前的資料庫。 如果未指定， *plan_guide_name* 預設為 Null。  
  
 DROP  
 卸載 *plan_guide_name*所指定的計劃指南。 在卸除計畫指南之後，未來執行先前符合計畫指南的查詢時，不會受計畫指南的影響。  
  
 DROP ALL  
 卸除目前資料庫中的所有計畫指南。 如果指定 DROP ALL，則無法指定**N '**_plan_guide_name_ 。  
  
 DISABLE  
 停用 *plan_guide_name*所指定的計劃指南。 在停用計畫指南之後，未來執行先前符合計畫指南的查詢時，不會受計畫指南的影響。  
  
 DISABLE ALL  
 停用目前資料庫中的所有計畫指南。 當指定 DISABLE ALL 時，無法指定**N '**_plan_guide_name_ 。  
  
 ENABLE  
 啟用 *plan_guide_name*所指定的計劃指南。 計畫指南在啟用之後，可以符合適合的查詢。 依預設，在建立計畫指南時，會啟用計畫指南。  
  
 ENABLE ALL  
 啟用目前資料庫中的所有計畫指南。 當指定 ENABLE ALL 時，無法指定**N '**_plan_guide_name_**'**。  
  
## <a name="remarks"></a>備註  
 試圖卸除或修改計畫指南所參考的函數、預存程序或 DML 觸發程序，不論是已啟用或已停用，都會造成錯誤。  
  
 停用已停用的計畫指南，或啟用已啟用的計畫指南，都沒有作用，執行時也不會發生錯誤。  
  
 並非所有版本都可使用計劃指南 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2016 版本和支援的功能](../../sql-server/editions-and-components-of-sql-server-2016.md)。 不過，您可以在任何版本的中使用 DROP 或 DROP ALL 選項來執行 **sp_control_plan_guide** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="permissions"></a>權限  
 若要在 object (的計劃指南（指定** @type = '** object **'** ）上執行**sp_control_plan_guide** ，) 需要計劃指南所參考之物件的 ALTER 許可權。 所有其他計畫指南都需要 ALTER DATABASE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-enabling-disabling-and-dropping-a-plan-guide"></a>A. 啟用、停用和卸除計畫指南  
 下列範例會建立一份計畫指南，以及停用、啟用再卸除這份計畫指南。  
  
```  
--Create a procedure on which to define the plan guide.  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country;  
END  
GO  
--Create the plan guide.  
EXEC sp_create_plan_guide N'Guide3',  
    N'SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country',  
    N'OBJECT',  
    N'Sales.GetSalesOrderByCountry',  
    NULL,  
    N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
GO  
--Disable the plan guide.  
EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
GO  
--Enable the plan guide.  
EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
GO  
--Drop the plan guide.  
EXEC sp_control_plan_guide N'DROP', N'Guide3';  
```  
  
### <a name="b-disabling-all-plan-guides-in-the-current-database"></a>B. 停用目前資料庫中的所有計畫指南  
 下列範例會停用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的所有計畫指南。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_control_plan_guide N'DISABLE ALL';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [計畫指南](../../relational-databases/performance/plan-guides.md)  
  
