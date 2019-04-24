---
title: DROP WORKLOAD 分類器 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
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
ms.assetid: ''
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: a9ef53323d77f1439df5daf0fedc669fe380cb3f
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59581512"
---
# <a name="drop-workload-classifier-transact-sql-preview"></a>DROP WORKLOAD 分類器 (Transact-SQL) (預覽)

> [!Note]
> 工作負載分類可在 SQL Data Warehouse Gen2 上以預覽形式取得。 「工作負載管理分類與重要性」預覽適用於發行日期為 2019 年 4 月 9 日或之後的組建。  使用者應避免使用早於此日期之前的組建進行工作負載管理測試。  若要判斷您的組建是否能使用工作負載管理，請在連線至您的 SQL 資料倉儲執行個體時，執行 select @ @version。

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

卸除現有使用者定義的「工作負載管理分類器」。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法  

```
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>引數

*classifier_name*  
指定用來識別工作負載分類器的名稱。  classifier_name 是一種 sysname。  它的長度最多可以是 128 個字元，且在執行個體內必須是唯一的。
  
## <a name="remarks"></a>Remarks

系統工作負載分類器不允許使用 DROP WORKLOAD CLASSIFIER 陳述式。

如果要求在執行中或在要求佇列中處於暫止狀態，它們會保留其分類，因此可以立即卸除分類器。  卸除分類器並以不同的重要性加以重建，將不會影響已經分類的要求。

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
[SQL 資料倉儲工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
