---
title: sys.sql_feature_restrictions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_sql_feature_restrictions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_feature_restrictions catalog view
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 9ffdcaaefe60c1972993501814cae555fb907f26
ms.sourcegitcommit: 561cee96844b82ade6cf543a228028ad5c310768
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66506996"
---
# <a name="syssqlfeaturerestrictions-transact-sql"></a>sys.sql_feature_restrictions & Amp;#40;transact-SQL&AMP;#41;

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

傳回資料庫中的每個限制的一個資料列。
  
| 資料行名稱 | 資料類型 | 描述 |
|-------------|-----------|-------------|
| class       | nvarchar(128) | 要套用這項限制的物件類別 |
| 物件 (object)      | nvarchar(256) | 這項限制適用於的物件的名稱 |
| 功能     | nvarchar(128) | 受限的功能 |
  
## <a name="remarks"></a>備註

目前的下列功能可以限制：

| 功能          | 描述 |
|------------------|-------------|
| N'ErrorMessages' | 限制時，將會遮罩處理的錯誤訊息中的任何使用者資料。 |
| N'Waitfor'       | 限制時，此命令會立即傳回且沒有任何延遲。 |
  
## <a name="permissions"></a>Permissions

正在執行的主體必須具有`CONTROL`資料庫的權限。
  
## <a name="see-also"></a>另請參閱

 [功能限制](../../relational-databases/security/feature-restrictions.md)