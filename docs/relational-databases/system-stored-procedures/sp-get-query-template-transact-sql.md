---
title: sp_get_query_template （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_get_query_template
- sp_get_query_template_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_query_template
ms.assetid: 85e9bef7-2417-41a8-befa-fe75507d9bf2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0da844225d9a87cbc0c7b6cf06d1bbea108f2d61
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757904"
---
# <a name="sp_get_query_template-transact-sql"></a>sp_get_query_template (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  傳回查詢的參數化格式。 傳回的結果會模擬使用強制參數化所產生之參數化形式的查詢。 sp_get_query_template 主要用於當您建立 TEMPLATE 計畫指南時。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_get_query_template  
   [ @querytext = ] N'query_text'  
   , @templatetext OUTPUT   
   , @parameters OUTPUT   
```  
  
## <a name="arguments"></a>引數  
 '*query_text*'  
 這是要產生參數化版本的查詢。 '*query_text*' 必須以單引號括住，且前面加上 N Unicode 規範。 N '*query_text*' 是指派給參數的值 @querytext 。 這是**Nvarchar （max）** 類型。  
  
 @templatetext  
 是**Nvarchar （max）** 類型的輸出參數，如所示，以字串常值的形式接收*query_text*的參數化格式。  
  
 @parameters  
 是**Nvarchar （max）** 類型的輸出參數，如所示，用來接收已參數化之參數名稱和資料類型的字串常值 @templatetext 。  
  
## <a name="remarks"></a>備註  
 當發生下列情況時，sp_get_query_template 會傳回錯誤：  
  
-   它不會將*query_text*中的任何常數常值參數化。  
  
-   *query_text*為 Null，而不是 Unicode 字串、語法無效或無法編譯。  
  
 如果 sp_get_query_template 傳回錯誤，則不會修改 @templatetext 和 @parameters 輸出參數的值。  
  
## <a name="permissions"></a>權限  
 需要 public 資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會傳回包含兩個常數常值之參數化形式的查詢。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @my_templatetext nvarchar(max)  
DECLARE @my_parameters nvarchar(max)  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
        FROM Production.ProductModel pm   
        INNER JOIN Production.ProductInventory pi  
        ON pm.ProductModelID = pi.ProductID  
        WHERE pi.ProductID = 2  
        GROUP BY pi.ProductID, pi.Quantity  
        HAVING SUM(pi.Quantity) > 400',  
@my_templatetext OUTPUT,  
@my_parameters OUTPUT;  
SELECT @my_templatetext;  
SELECT @my_parameters;  
```  
  
 以下是 `@my_templatetext``OUTPUT` 參數的參數化結果：  
  
 `select pi . ProductID , SUM ( pi . Quantity ) as Total`  
  
 `from Production . ProductModel pm`  
  
 `inner join Production . ProductInventory pi`  
  
 `on pm . ProductModelID = pi . ProductID`  
  
 `where pi . ProductID = @0`  
  
 `group by pi . ProductID , pi . Quantity`  
  
 `having SUM ( pi . Quantity ) > 400`  
  
 請注意，第一個常數常值 `2` 會轉換成參數。 第二個常值 `400` 並未轉換，因為它在 `HAVING` 子句內。 當 ALTER DATABASE 的 PARAMETERIZATION 選項設為 FORCED 時，sp_get_query_template 傳回的結果會模擬參數化形式的查詢。  
  
 以下是 `@my_parameters OUTPUT` 參數的參數化結果：  
  
```  
@0 int  
```  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的快速修復工程、Service Pack 和版本升級之間，sp_get_query_template 輸出中的參數順序和命名可能會不同。 升級也可能造成針對相同查詢參數化不同組的常數常值，在兩個輸出參數的結果中，可能會套用不同的間距。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料庫引擎預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [使用計畫指南指定查詢參數化行為](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)  
  
  
