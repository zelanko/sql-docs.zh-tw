---
title: CREATE WORKLOAD 分類器 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
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
ms.openlocfilehash: 327d0b0929305561a7be55b38b9d6cb97299e088
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938873"
---
# <a name="create-workload-classifier-transact-sql"></a>CREATE WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

建立「工作負載管理分類器」。  分類器會根據分類器陳述式定義中指定的參數，將連入要求指派給工作負載群組，並指派重要性。  每個提交的要求都會評估分類器。  如果要求與分類器不相符，則會將其指派給預設的工作負載群組。  預設工作負載群組為 smallrc 資源類別。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法

```
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    ( WORKLOAD_GROUP = 'name'  
     ,MEMBERNAME = 'security_account'
 [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL (default) | ABOVE_NORMAL | HIGH }])
[;]
```

## <a name="arguments"></a>引數

 *classifier_name*  
 指定用來識別工作負載分類器的名稱。  classifier_name 是一種 sysname。  它的長度最多可以是 128 個字元，且在執行個體內必須是唯一的。

WORKLOAD_GROUP = *'name'* 分類器規則符合條件時，name 會將要求對應至工作負載群組。  name 是一種 sysname。  它的長度最多可以是 128 個字元，且在分類器建立時必須是有效的工作負載群組名稱。

WORKLOAD_GROUP 應該對應至現有的資源類別：

|靜態資源類別|靜態資源類別|
|------------------------|-----------------------|
|staticrc10|smallrc|
|staticrc20|mediumrc|
|staticrc30|largerc|
|staticrc40|xlargerc|
|staticrc50||
|staticrc60||
|staticrc70||
|staticrc80||

MEMBERNAME = *'security_account'* 這是要新增至角色的安全性帳戶。  Security_account 是一種 sysname，沒有預設值。 Security_account 可以是資料庫使用者、資料庫角色、Azure Active Directory 登入或 Azure Active Directory 群組。

IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } 指定要求的相對重要性。  重要性為下列其中一項：

- LOW
- BELOW_NORMAL
- NORMAL (預設)
- ABOVE_NORMAL
- HIGH  

重要性會影響所排定要求的順序，進而授與資源和鎖定的優先存取權。

如果使用者是多個角色的成員，且被指派了不同的資源類別或在多個分類器中相符，該使用者將獲得最高的資源類別指派。 如需詳細資訊，請參閱[工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification#classification-precedence)

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

[DROP WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-classifier-transact-sql.md)</br>
目錄檢視 [sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)</br>
目錄檢視 [sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)
[SQL 資料倉儲分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
