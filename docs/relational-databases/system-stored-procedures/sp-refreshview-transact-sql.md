---
title: sp_refreshview (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_refreshview
- sp_refreshview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refreshview
ms.assetid: 9ce1d07c-ee66-4a83-8c73-cd2cc104dd08
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed5f50b9b95f2f156632fb14c2cd471ef010bcac
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031476"
---
# <a name="sprefreshview-transact-sql"></a>sp_refreshview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新指定非結構描述繫結檢視的中繼資料。 檢視所依賴的基礎物件變更之後，檢視的保存中繼資料也可能會過期。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_refreshview [ @viewname = ] 'viewname'   
```  
  
## <a name="arguments"></a>引數  
 [  **@viewname=** ] **'***viewname***'**  
 這是檢視的名稱。 *viewname*已**nvarchar**，沒有預設值。 *viewname*可以是多部分識別碼，但只能參考目前資料庫中的檢視。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)  
  
## <a name="remarks"></a>備註  
 如果未以 schemabinding 來建立檢視**sp_refreshview**檢視會影響檢視定義的物件進行變更時，應該執行。 否則，在查詢檢視時，可能會產生非預期的結果。  
  
## <a name="permissions"></a>Permissions  
 必須對檢視具備 ALTER 權限，以及對檢視資料行所參考的 Common Language Runtime (CLR) 使用者自訂類型和 XML 結構描述集合，具備 REFERENCES 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-updating-the-metadata-of-a-view"></a>A. 更新檢視的中繼資料  
 下列範例會重新整理 `Sales.vIndividualCustomer` 檢視的中繼資料。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sp_refreshview N'Sales.vIndividualCustomer';  
```  
  
### <a name="b-creating-a-script-that-updates-all-views-that-have-dependencies-on-a-changed-object"></a>B. 建立可更新所有對於已變更物件具有相依性之檢視的指令碼  
 假設資料表 `Person.Person` 是以會影響在任何檢視上建立的定義之方式來變更。 下列範例建立了一個指令碼，針對所有對資料表 `Person.Person` 有相依性的檢視來重新整理中繼資料。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT 'EXEC sp_refreshview ''' + name + ''''   
FROM sys.objects AS so   
INNER JOIN sys.sql_expression_dependencies AS sed   
    ON so.object_id = sed.referencing_id   
WHERE so.type = 'V' AND sed.referenced_id = OBJECT_ID('Person.Person');  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_refreshsqlmodule &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md)  
  
  
