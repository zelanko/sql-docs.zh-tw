---
title: sp_settriggerorder (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bef1fdf427c6bc510e77f8df55f3281d5b5db6cd
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "33263559"
---
# <a name="spsettriggerorder-transact-sql"></a>sp_settriggerorder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定第一個或最後一個引發的 AFTER 觸發程序。 在第一個及最後一個觸發程序之間啟動的 AFTER 觸發程序，會以未定義的順序執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@triggername=** ] **'**[ *triggerschema ***。**]*triggername * * * '**  
 這是要設定或變更順序的觸發程序及所屬結構描述 (如果適用) 的名稱。 [*triggerschema ***。**]* triggername * 是**sysname**。 如果名稱未對應於觸發程序，或名稱對應於 INSTEAD OF 觸發程序，程序會傳回錯誤。 *triggerschema*不能指定 DDL 或登入觸發程序。  
  
 [ **@order=** ] **'***value***'**  
 這是觸發程序的新順序設定。 *值*是**varchar （10)** 和它可以是下列值之一。  
  
> [!IMPORTANT]  
>  **第一個**和**最後**觸發程序必須是兩個不同的觸發程序。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**第一個**|最先引發觸發程序。|  
|**最後一個**|最後引發觸發程序。|  
|**無**|觸發程序的引發，沒有任何既定順序。|  
  
 [  **@stmttype=** ] **'***statement_type***'**  
 指定可以引發觸發程序的 SQL 陳述式。 *statement_type*是**varchar （50)** 而且可以是 INSERT、 UPDATE、 DELETE、 登入，或任何[!INCLUDE[tsql](../../includes/tsql-md.md)]中所列的陳述式事件[DDL 事件](../../relational-databases/triggers/ddl-events.md)。 您不能指定事件群組。  
  
 觸發程序可以指定為**第一個**或**最後**該觸發程序已定義為該陳述式類型的觸發程序之後，才陳述式類型的觸發程序。 例如，觸發**TR1**可指定**第一個**資料表上的插入**T1**如果**TR1**定義為 INSERT 觸發程序。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]如果傳回錯誤**TR1**，其中已定義為 INSERT 觸發程序，只會設定為**第一個**，或**最後**，UPDATE 陳述式的觸發程序。 如需詳細資訊，請參閱＜備註＞一節。  
  
 **@namespace=** { **'DATABASE'** | **'SERVER'** |NULL}  
 當*triggername* DDL 觸發程序， **@namespace**指定是否*triggername*建立使用資料庫範圍或伺服器範圍。 如果*triggername*登入觸發程序，必須指定伺服器。 如需有關 DDL 觸發程序範圍的詳細資訊，請參閱[DDL 觸發程序](../../relational-databases/triggers/ddl-triggers.md)。 如果未指定，或指定 NULL，則*triggername* DML 觸發程序。  
  
||  
|-|  
|SERVER 適用於：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 和 1 (失敗)  
  
## <a name="remarks"></a>備註  
  
## <a name="dml-triggers"></a>DML 觸發程序  
 可以有只有一個**第一個**一個**最後**單一資料表上每個陳述式的觸發程序。  
  
 如果**第一個**資料表、 資料庫或伺服器上已定義觸發程序，您不能指定新的觸發程序，當做**第一個**針對相同的資料表、 資料庫或伺服器的相同*statement_type*. 這項限制也適用於**最後**觸發程序。  
  
 複寫會為包含在即時更新或佇列式更新訂閱的資料表，自動產生第一個觸發程序。 複寫需要觸發程序是第一個觸發程序。 當您嘗試將含有第一個觸發程序的資料表包括在立即更新或佇列更新訂閱中，複寫會引發錯誤。 如果您嘗試在資料表已加入訂閱後，將觸發程序變成第一個觸發程序，則 **sp_settriggerorder** 會傳回錯誤。 如果您使用 ALTER TRIGGER 複寫的觸發程序，或使用**sp_settriggerorder**複寫觸發程序來變更**最後**或**無**觸發程序，訂閱會執行無法正確運作。  
  
## <a name="ddl-triggers"></a>DDL 觸發程序  
 如果資料庫範圍的 DDL 觸發程序和具有伺服器範圍的 DDL 觸發程序存在於相同的事件，您可以指定這兩個觸發程序是**第一個**觸發程序或**最後**觸發程序。 不過，伺服器範圍的觸發程序一定會先觸發。 一般來說，存在於相同事件上之 DDL 觸發程序的執行順序如下：  
  
1.  伺服器層級觸發程序標示**第一個**。  
  
2.  其他伺服器層級觸發程序。  
  
3.  伺服器層級觸發程序標示**最後**。  
  
4.  資料庫層級觸發程序標示**第一個**。  
  
5.  其他資料庫層級觸發程序。  
  
6.  資料庫層級觸發程序標示**最後**。  
  
## <a name="general-trigger-considerations"></a>一般觸發程序考量  
 如果 ALTER TRIGGER 陳述式變更第一個或最後一個觸發程序**第一個**或**最後**卸除原本設定的觸發程序的屬性和值會取代**無**。 使用順序值必須重設**sp_settriggerorder**。  
  
 如果相同的觸發程序必須指定為一個以上的陳述式類型的第一個或最後一個順序**sp_settriggerorder**必須執行每個陳述式類型。 此外，觸發程序必須先定義陳述式類型之前被指定為**第一個**或**最後**觸發程序引發的陳述式類型。  
  
## <a name="permissions"></a>Permissions  
 若要設定具有伺服器範圍 (在 ON ALL SERVER 上建立) 的 DDL 觸發程序或登入觸發程序的順序，便需要 CONTROL SERVER 權限。  
  
 若要設定具有資料庫範圍 (建立時設定 ON DATABASE) 的 DDL 觸發程序順序，便需要 ALTER ANY DATABASE DDL TRIGGER 權限。  
  
 設定 DML 觸發程序的順序時，需要觸發程序定義所在之資料表或檢視的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>A. 設定 DML 觸發程序的引發順序  
 下列範例將 `uSalesOrderHeader` 觸發程序指定為在 `UPDATE` 資料表中發生 `Sales.SalesOrderHeader` 作業之後，所引發的第一個觸發程序。  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'Sales.uSalesOrderHeader', @order='First', @stmttype = 'UPDATE';  
```  
  
### <a name="b-setting-the-firing-order-for-a-ddl-trigger"></a>B. 設定 DDL 觸發程序的引發順序  
 下列範例將 `ddlDatabaseTriggerLog` 觸發程序指定為 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫發生 `ALTER_TABLE` 事件之後，所引發的第一個觸發程序。  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'ddlDatabaseTriggerLog', @order='First', @stmttype = 'ALTER_TABLE', @namespace = 'DATABASE';  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
