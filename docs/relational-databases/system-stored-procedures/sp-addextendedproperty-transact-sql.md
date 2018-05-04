---
title: sp_addextendedproperty (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addextendedproperty
- sp_addextendedproperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproperty
ms.assetid: 565483ea-875b-4133-b327-d0006d2d7b4c
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0cebcbdbc01a96af839450865bb6e7c924027409
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spaddextendedproperty-transact-sql"></a>sp_addextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將新的擴充屬性加入資料庫物件中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addextendedproperty  
    [ @name = ] { 'property_name' }  
    [ , [ @value = ] { 'value' }   
        [ , [ @level0type = ] { 'level0_object_type' }   
          , [ @level0name = ] { 'level0_object_name' }   
                [ , [ @level1type = ] { 'level1_object_type' }   
                  , [ @level1name = ] { 'level1_object_name' }   
                        [ , [ @level2type = ] { 'level2_object_type' }   
                          , [ @level2name = ] { 'level2_object_name' }   
                        ]   
                ]  
        ]   
    ]   
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ @name ] = {'*property_name*'}  
 這是要加入的屬性名稱。 *property_name*是**sysname**不能是 NULL。 名稱也可包含空白或非英數字元字串，以及二進位值。  
  
 [ @value=] {'*值*'}  
 這是與屬性相關聯的值。 *值*是**sql_variant**，預設值是 NULL。 *value* 的大小不能超過 7,500 個位元組。  
  
 [ @level0type=] {'*level0_object_type*'}  
 這是層級 0 物件的類型。 *level0_object_type*是**varchar （128)**，預設值是 NULL。  
  
 有效輸入如下：ASSEMBLY、CONTRACT、EVENT NOTIFICATION、FILEGROUP、MESSAGE TYPE、PARTITION FUNCTION、PARTITION SCHEME、REMOTE SERVICE BINDING、ROUTE、SCHEMA、SERVICE、USER、TRIGGER、TYPE、PLAN GUIDE 和 NULL。  
  
> [!IMPORTANT]  
>  將 USER 指定為層級 1 類型物件擴充屬性中之層級 0 類型的功能，將在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中移除。 請改用 SCHEMA 做為層級 0 類型。 例如，在資料表上定義擴充屬性時，請指定資料表的結構描述代替使用者名稱。 將 TYPE 指定為層級 0 類型的功能，將在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中移除。 如果是 TYPE，請使用 SCHEMA 當做層級 0 類型，並使用 TYPE 當做層級 1 類型。  
  
 [ @level0name=] {'*level0_object_name*'}  
 這是所指定之層級 0 物件類型的名稱。 *level0_object_name*是**sysname**預設值是 NULL。  
  
 [ @level1type=] {'*level1_object_type*'}  
 這是層級 1 物件的類型。 *level1_object_type*是**varchar （128)**，預設值是 NULL。 有效輸入如下：AGGREGATE、DEFAULT、FUNCTION、LOGICAL FILE NAME、PROCEDURE、QUEUE、RULE、SYNONYM、TABLE、TABLE_TYPE、TYPE、VIEW、XML SCHEMA COLLECTION 和 NULL。  
  
 [ @level1name=] {'*level1_object_name*'}  
 這是所指定之層級 1 物件類型的名稱。 *level1_object_name*是**sysname**，預設值是 NULL。  
  
 [ @level2type=] {'*level2_object_type*'}  
 這是層級 2 物件的類型。 *level2_object_type*是**varchar （128)**，預設值是 NULL。 有效輸入如下：COLUMN、CONSTRAINT、EVENT NOTIFICATION、INDEX、PARAMETER、TRIGGER 和 NULL。  
  
 [ @level2name=] {'*level2_object_name*'}  
 這是所指定之層級 2 物件類型的名稱。 *level2_object_name*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 為了指定擴充屬性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的物件分為三種層級：0、1 與 2。 層級 0 是最高層級，且定義為包含在資料庫範圍的物件。 層級 1 物件包含在結構描述或使用者範圍中，層級 2 物件包含在層級 1 物件中。 任何這些層級的物件都可以定義擴充屬性。  
  
 對一個層級中物件的參考必須用擁有或包含其較高層級物件的名稱來限定。 例如，當您將擴充屬性加入至資料表資料行 (層級 2) 時，您也必須指定包含該資料行的資料表名稱 (層級 1) 和包含該資料表的結構描述 (層級 0)。  
  
 如果所有物件類型和名稱都是 NULL，屬性屬於目前資料庫本身。  
  
 擴充屬性不得用於系統物件、使用者自訂資料庫範圍外的物件，或未列在引數中做為有效輸入的物件。  
  
 記憶體最佳化資料表上不允許的擴充的屬性。  
  
## <a name="replicating-extended-properties"></a>複寫擴充屬性  
 只在發行者與訂閱者之間的初始同步處理中複寫擴充屬性。 如果您在初始同步處理之後加入或修改擴充屬性，就不會複寫這項變更。 如需如何複寫資料庫物件的詳細資訊，請參閱[發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
## <a name="schema-vs-user"></a>結構描述與使用者  
 不建議您在將擴充屬性套用至資料庫物件時指定 USER 當做層級 0 類型，因為這會造成名稱解析模稜兩可。 例如，假設使用者 Mary 擁有兩個結構描述 (Mary 和 MySchema)，而這兩個結構描述都包含一個名為 MyTable 的資料表。 如果 Mary 將擴充的屬性加入至 MyTable 資料表，並指定 **@level0type = N'USER'**，  **@level0name = Mary**，並不清楚哪個資料表擴充的屬性套用。 為了維持回溯相容性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將套用屬性至包含在名為 Mary 之結構描述中的資料表。  
  
## <a name="permissions"></a>Permissions  
 db_owner 和 db_ddladmin 固定資料庫角色的成員可將擴充屬性加入至任何物件，但下列為例外狀況：db_ddladmin 不能將屬性加入至資料庫本身或加入至使用者或角色。  
  
 使用者可將擴充屬性加入至他們擁有的物件或他們具有 ALTER 或 CONTROL 權限的物件。  
  
## <a name="examples"></a>範例  
  
### <a name="a-adding-an-extended-property-to-a-database"></a>A. 將擴充屬性加入至資料庫  
 `'Caption'` 下列範例將一個含有 `'AdventureWorks2012 Sample OLTP Database'` 值的屬性名稱 `AdventureWorks2012` 加入至 範例資料庫。  
  
```  
USE AdventureWorks2012;  
GO  
--Add a caption to the AdventureWorks2012 Database object itself.  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'AdventureWorks2012 Sample OLTP Database';  
```  
  
### <a name="b-adding-an-extended-property-to-a-column-in-a-table"></a>B. 將擴充屬性加入至資料表中的資料行  
 `PostalCode` 下列範例將標題屬性加入至 `Address`資料表中的 資料行。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'Postal code is a required column.',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table',  @level1name = 'Address',  
@level2type = N'Column', @level2name = 'PostalCode';  
GO  
```  
  
### <a name="c-adding-an-input-mask-property-to-a-column"></a>C. 將輸入遮罩屬性加入至資料行  
 `99999 or 99999-9999 or #### ###`下列範例將 ' `PostalCode` ' 輸入遮罩屬性加入至 `Address`資料表中的 資料行。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Input Mask ', @value = '99999 or 99999-9999 or #### ###',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table', @level1name = 'Address',   
@level2type = N'Column',@level2name = 'PostalCode';  
GO  
```  
  
### <a name="d-adding-an-extended-property-to-a-filegroup"></a>D. 將擴充屬性加入至檔案群組  
 `PRIMARY` 下列範例會將擴充屬性加入至  檔案群組中。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Primary filegroup for the AdventureWorks2012 sample database.',   
@level0type = N'FILEGROUP', @level0name = 'PRIMARY';  
GO  
```  
  
### <a name="e-adding-an-extended-property-to-a-schema"></a>E. 將擴充屬性加入至結構描述  
 `HumanResources` 下列範例會將擴充屬性加入至  結構描述中。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',  
@value = N'Contains objects related to employees and departments.',  
@level0type = N'SCHEMA',   
@level0name = 'HumanResources';  
```  
  
### <a name="f-adding-an-extended-property-to-a-table"></a>F. 將擴充屬性加入至資料表  
 `Address` 下列範例會將擴充屬性加入至 `Person` 結構描述中的  資料表。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Street address information for customers, employees, and vendors.',   
@level0type = N'SCHEMA', @level0name = 'Person',  
@level1type = N'TABLE',  @level1name = 'Address';  
GO  
```  
  
### <a name="g-adding-an-extended-property-to-a-role"></a>G. 將擴充屬性加入至角色  
 下列範例會建立應用程式角色並將擴充屬性加入至該角色。  
  
```  
USE AdventureWorks2012;   
GO  
CREATE APPLICATION ROLE Buyers  
WITH Password = '987G^bv876sPY)Y5m23';   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Application Role for the Purchasing Department.',  
@level0type = N'USER',  
@level0name = 'Buyers';  
```  
  
### <a name="h-adding-an-extended-property-to-a-type"></a>H. 將擴充屬性加入至類型  
 下列範例會將擴充屬性加入至類型中。  
  
```  
USE AdventureWorks2012;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Data type (alias) to use for any column that represents an order number. For example a sales order number or purchase order number.',   
@level0type = N'SCHEMA',   
@level0name = N'dbo',   
@level1type = N'TYPE',   
@level1name = N'OrderNumber';  
```  
  
### <a name="i-adding-an-extended-property-to-a-user"></a>I. 將擴充屬性加入至使用者  
 下列範例會建立使用者並將擴充屬性加入至該使用者。  
  
```  
USE AdventureWorks2012;   
GO  
CREATE USER CustomApp WITHOUT LOGIN ;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'User for an application.',   
@level0type = N'USER',   
@level0name = N'CustomApp';  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.fn_listextendedproperty &#40;Transact SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)  
  
  
