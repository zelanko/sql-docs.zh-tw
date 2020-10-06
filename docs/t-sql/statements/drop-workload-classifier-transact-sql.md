---
description: DROP WORKLOAD CLASSIFIER (Transact-SQL)
title: DROP WORKLOAD 分類器 (Transact-SQL) | Microsoft Docs
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
- DROP_WORKLOAD_CLASSIFIER_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD CLASSIFIER statement
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 6094ab4bb81556ce630730eb35f275dcb58071ab
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2020
ms.locfileid: "91669063"
---
# <a name="drop-workload-classifier-transact-sql"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

卸除現有使用者定義的工作負載管理分類器。  如果要求在執行中或在要求佇列中處於暫止狀態，它們會保留其分類，因此可以立即卸除分類器。 卸除分類器並以不同的重要性加以重建，將不會影響已經分類的要求。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法  

```syntaxsql
DROP WORKLOAD CLASSIFIER classifier_name;
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="arguments"></a>引數

*classifier_name*  
指定用來識別工作負載分類器的名稱。
  
## <a name="permissions"></a>權限

需要 CONTROL DATABASE 權限。  
  
## <a name="examples"></a>範例

下列範例會卸除名為 `wgcELTROLE` 的工作負載分類器。  

```sql
DROP WORKLOAD CLASSIFIER wgcELTRole;
```

> [!NOTE]
> 提交時沒有相符分類器的要求會分類到預設工作負載群組。  預設工作負載群組為 smallrc 資源類別。
  
## <a name="see-also"></a>另請參閱

[CREATE WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-classifier-transact-sql.md)</br>
[[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
