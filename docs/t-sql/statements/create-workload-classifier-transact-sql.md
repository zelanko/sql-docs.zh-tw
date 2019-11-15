---
title: CREATE WORKLOAD 分類器 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- CREATE WORKLOAD CLASSIFIER
- CREATE_WORKLOAD_CLASSIFIER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 5ee3b24f1c2b85d2c4966b632257ac941c9776ee
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632890"
---
# <a name="create-workload-classifier-transact-sql"></a>CREATE WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

建立用於工作負載管理的分類器物件。  分類器會根據分類器陳述式定義中指定的參數，將連入要求指派給工作負載群組。  每個提交的要求都會評估分類器。  如果要求與分類器不相符，則會將其指派給預設的工作負載群組。  預設工作負載群組為 smallrc 資源類別。

> [!NOTE]
> 工作負載分類器會取代 sp_addrolemember 資源類別指派。  建立工作負載分類器之後，請執行 sp_droprolemember 以移除任何多餘的資源類別對應。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法

```
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    (   WORKLOAD_GROUP = ‘name’  
    ,   MEMBERNAME = ‘security_account’ 
[ [ , ] WLM_LABEL = ‘label’ ]  
[ [ , ] WLM_CONTEXT = ‘context’ ]  
[ [ , ] START_TIME = ‘HH:MM’ ]  
[ [ , ] END_TIME = ‘HH:MM’ ]  
  
[ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]) 
[;]
```

## <a name="arguments"></a>引數

 *classifier_name*  
 指定用來識別工作負載分類器的名稱。  classifier_name 是一種 sysname。  它的長度最多可以是 128 個字元，且在執行個體內必須是唯一的。

 *WORKLOAD_GROUP* =  *'name'*    
 當分類器規則符合條件時，name 會將要求對應至工作負載群組。  name 是一種 sysname。  它的長度最多可以是 128 個字元，且在分類器建立時必須是有效的工作負載群組名稱。

 可用的工作負載群組可以在 [sys.workload_management_workload_groups](/sql/relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md?view=azure-sqldw-latest) 目錄檢視中找到。

 *MEMBERNAME* ='security_account'*    
 這是加入角色的安全性帳戶。  Security_account 是一種 sysname，沒有預設值。 Security_account 可以是資料庫使用者、資料庫角色、Azure Active Directory 登入或 Azure Active Directory 群組。
 
 *WLM_LABEL*   
 指定可分類要求的標籤值。  Label 是 nvarchar(255) 類型的選擇性參數。  在要求中使用 [OPTION (LABEL)](/azure/sql-data-warehouse/sql-data-warehouse-develop-label)，以符合分類器設定。

範例：

```sql
CREATE WORKLOAD CLASSIFIER wcELTLoads WITH  
( WORKLOAD_GROUP = 'wgDataLoad'
 ,MEMBERNAME     = 'ELTRole'  
 ,WLM_LABEL      = 'dimension_loads' )

SELECT COUNT(*) 
  FROM DimCustomer
  OPTION (LABEL = 'dimension_loads')
```

*WLM_CONTEXT*  
指定可分類要求的工作階段內容值。  context 是 nvarchar(255) 類型的選擇性參數。  在提交設定工作階段內容的要求之前，使用變數名稱等於 `wlm_context` 的 [sys.sp_set_session_context](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md?view=azure-sqldw-latest)。

範例：

```sql
CREATE WORKLOAD CLASSIFIER wcDataLoad WITH  
( WORKLOAD_GROUP = 'wgDataLoad'
 ,MEMBERNAME     = 'ELTRole'
 ,WLM_CONTEXT    = 'dim_load' )
 
--set session context
EXEC sys.sp_set_session_context @key = 'wlm_context', @value = 'dim_load'

--run multiple statements using the wlm_context setting
SELECT COUNT(*) FROM stg.daily_customer_load
SELECT COUNT(*) FROM stg.daily_sales_load

--turn off the wlm_context session setting
EXEC sys.sp_set_session_context @key = 'wlm_context', @value = null
```

*START_TIME* 和 *END_TIME*  
指定要求可以分類的 start_time 和 end_time。  start_time 和 end_time 都是 UTC 時區的 HH:MM 格式。  start_time and end_time 必須同時指定。

範例：

```sql
CREATE WORKLOAD CLASSIFIER wcELTLoads WITH  
( WORKLOAD_GROUP = 'wgDataLoads'
 ,MEMBERNAME     = 'ELTRole'  
 ,START_TIME     = '22:00'
 ,END_TIME       = '02:00' )
```

*IMPORTANCE* = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }  
指定要求的相對重要性。  重要性為下列其中一項：

- LOW
- BELOW_NORMAL
- NORMAL (預設)
- ABOVE_NORMAL
- HIGH  

如果未指定重要性，則會使用工作負載群組的重要性設定。  預設工作負載群組重要性是 NORMAL。  重要性會影響所排定要求的順序，進而授與資源和鎖定的優先存取權。

## <a name="classification-parameter-precedence"></a>分類參數優先順序

要求可以符合多個分類器。  分類器參數中有優先順序。  首先使用優先順序較高的對應分類器來指派工作負載群組和重要性。  優先順序如下所示：
1. USER
2. ROLE
3. WLM_LABEL
4. WLM_SESSION
5. START_TIME/END_TIME

請考慮下列分類器設定。

```sql
CREATE WORKLOAD CLASSIFIER classiferA WITH  
( WORKLOAD_GROUP = 'wgDashboards'  
 ,MEMBERNAME     = 'userloginA'
 ,IMPORTANCE     = HIGH
 ,WLM_LABEL      = 'salereport' )

CREATE WORKLOAD CLASSIFIER classiferB WITH  
( WORKLOAD_GROUP = 'wgUserQueries'  
 ,MEMBERNAME     = 'userloginA'
 ,IMPORTANCE     = LOW
 ,START_TIME     = '18:00')
 ,END_TIME       = '07:00' )
```

使用者 `userloginA` 是針對這兩個分類器所設定。  如果 userloginA 在 UTC 下午 6 點和上午 7 點之間執行帶有等於 `salesreport` 的標籤的查詢，則該要求將被分類為具有高重要性的 wgDashboards 工作負載群組。  預期的情況可能是針對非工作時間報告將要求分類為重要性較低的 wgUserQueries，但是 WLM_LABEL 的優先順序高於 START_TIME/END_TIME。  在此情況下，您可以將 START_TIME/END_TIME 新增至 classiferA。

 如需詳細資訊，請參閱[工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification#classification-precedence)。

## <a name="permissions"></a>權限

 需要 CONTROL DATABASE 權限。  
  
## <a name="examples"></a>範例

 下列範例會顯示如何建立名為 `wgcELTRole` 的工作負載分類器。 它會使用 staticrc20 工作負載群組、使用者 `ELTRole`，並將重要性設定為 `above_normal`。

```sql
CREATE WORKLOAD CLASSIFIER wgcELTRole
  WITH (WORKLOAD_GROUP = 'staticrc20'
       ,MEMBERNAME = 'ELTRole'
      ,IMPORTANCE = above_normal);
```

## <a name="see-also"></a>另請參閱

[SQL 資料倉儲分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)</br>
[DROP WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-classifier-transact-sql.md)</br>
[sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)</br>
[sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)

