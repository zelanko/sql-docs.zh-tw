---
title: "sp_updateextendedproperty (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_updateextendedproperty_TSQL
- sp_updateextendedproperty
dev_langs: TSQL
helpviewer_keywords: sp_updateextendedproperty
ms.assetid: 7f02360f-cb9e-48b4-b75f-29b4bc9ea304
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 284eb1e8d95ff94091df493048826e3a958ffb8c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spupdateextendedproperty-transact-sql"></a>sp_updateextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  更新現有擴充屬性的值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_updateextendedproperty  
    [ @name = ]{ 'property_name' }   
    [ , [ @value = ]{ 'value' }  
        [, [ @level0type = ]{ 'level0_object_type' }  
         , [ @level0name = ]{ 'level0_object_name' }  
              [, [ @level1type = ]{ 'level1_object_type' }  
               , [ @level1name = ]{ 'level1_object_name' }  
                     [, [ @level2type = ]{ 'level2_object_type' }  
                      , [ @level2name = ]{ 'level2_object_name' }  
                     ]  
              ]  
        ]  
    ]  
```  
  
## <a name="arguments"></a>引數  
 [ @name=] {'*property_name*'}  
 這是要更新的屬性名稱。 *property_name*是**sysname**，不能是 NULL。  
  
 [ @value=] {'*值*'}  
 這是與屬性相關聯的值。 *值*是**sql_variant**，預設值是 NULL。 大小*值*不能超過 7,500 位元組。  
  
 [ @level0type=] {'*level0_object_type*'}  
 使用者或使用者定義類型。 *level0_object_type*是**varchar （128)**，預設值是 NULL。 有效輸入如下： 組件、 合約、 EVENT NOTIFICATION、 檔案群組、 訊息類型、 資料分割函數、 資料分割配置、 計畫指南、 遠端服務繫結、 路由、 結構描述、 服務、 使用者、 觸發程序、 類型和 NULL。  
  
> [!IMPORTANT]  
>  在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，會移除層級 0 類型的 USER 和 TYPE。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。 請改用 SCHEMA 來當做層級 0 類型，而不是使用 USER。 如果是 TYPE，請使用 SCHEMA 當做層級 0 類型，並使用 TYPE 當做層級 1 類型。  
  
 [ @level0name=] {'*level0_object_name*'}  
 這是所指定之層級 1 物件類型的名稱。 *level0_object_name*是**sysname**預設值是 NULL。  
  
 [ @level1type=] {'*level1_object_type*'}  
 這是層級 1 物件的類型。 *level1_object_type*是**varchar （128)**預設值是 NULL。 有效輸入如下：AGGREGATE、DEFAULT、FUNCTION、LOGICAL FILE NAME、PROCEDURE、QUEUE、RULE、SYNONYM、TABLE、TABLE_TYPE、TYPE、VIEW、XML SCHEMA COLLECTION 和 NULL。  
  
 [ @level1name=] {'*level1_object_name*'}  
 這是所指定之層級 1 物件類型的名稱。 *level1_object_name*是**sysname**預設值是 NULL。  
  
 [ @level2type=] {'*level2_object_type*'}  
 這是層級 2 物件的類型。 *level2_object_type*是**varchar （128)**預設值是 NULL。 有效輸入如下：COLUMN、CONSTRAINT、EVENT NOTIFICATION、INDEX、PARAMETER、TRIGGER 和 NULL。  
  
 [ @level2name=] {'*level2_object_name*'}  
 這是所指定之層級 2 物件類型的名稱。 *level2_object_name*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 為了指定擴充屬性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的物件會分類成 3 個層級 (0、1 和 2)。 層級 0 是最高層級，定義為資料庫範圍所包含的物件。 層級 1 物件包含在結構描述或使用者範圍中，層級 2 物件包含在層級 1 物件中。 任何這些層級的物件都可以定義擴充屬性。 對一個層級中物件的參考必須用擁有或包含其較高層級物件的名稱來限定。  
  
 給定有效*property_name*和*值*，如果所有物件類型和名稱都是 null，則更新的屬性屬於目前的資料庫。  
  
## <a name="permissions"></a>Permissions  
 除了下列例外狀況，db_owner 和 db_ddladmin 固定資料庫角色的成員可以更新任何物件的擴充屬性：db_ddladmin 不能將屬性加入至資料庫本身，或加入至使用者或角色中。  
  
 使用者可以更新他們所擁有之物件，或他們有 ALTER 或 CONTROL 權限之物件的擴充屬性。  
  
## <a name="examples"></a>範例  
  
### <a name="a-updating-an-extended-property-on-a-column"></a>A. 更新資料行的擴充屬性  
 下列範例會更新 `Caption` 資料表 `ID` 資料行的 `T1` 屬性值。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
    @name = N'Caption'  
    ,@value = N'Employee ID'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
--Update the extended property.  
EXEC sp_updateextendedproperty   
    @name = N'Caption'  
    ,@value = 'Employee ID must be unique.'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
```  
  
### <a name="b-updating-an-extended-property-on-a-database"></a>B. 更新資料庫的擴充屬性  
 下列範例會先建立 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫的擴充屬性，再更新這個屬性的值。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample OLTP Database';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_updateextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample Database';  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [Database Engine 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.fn_listextendedproperty &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
