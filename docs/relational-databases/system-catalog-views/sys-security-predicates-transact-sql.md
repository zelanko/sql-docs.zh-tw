---
title: sys.databases security_predicates （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.SECURITY_PREDICATES
- SECURITY_PREDICATES
- SECURITY_PREDICATES_TSQL
- SYS.SECURITY_PREDICATES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_predicates catalog view
- security_predicates catalog view
ms.assetid: c7a2f28c-98da-463d-8b8a-8e5619e2c6a6
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6cf464370c5c2ca3f5075205c6783e9332309f12
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68135218"
---
# <a name="syssecurity_predicates-transact-sql"></a>sys.databases security_predicates （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  針對資料庫中的每個安全性述詞，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_id|**int**|包含這個述詞之安全性原則的識別碼。|  
|security_predicate_id|**int**|這個安全性原則內的述詞識別碼。|  
|target_object_id|**int**|安全性述詞所繫結之物件的識別碼。|  
|predicate_definition|**nvarchar(max)**|用來做為安全性述詞之函數的完整名稱，包括引數。 請注意，`schema.function` 名稱可正規化 (即逸出) 以維護一致性，就像是文字中的其他任何項目一樣。 例如：<br /><br /> `[dbo].[fn_securitypredicate]([wing], [startTime], [endTime])`|  
|predicate_type|**int**|安全性原則所使用的述詞類型：<br /><br /> 0 = 篩選述詞<br /><br /> 1 = 封鎖述詞|  
|predicate_type_desc|**nvarchar(60)**|安全性原則所使用的述詞類型：<br /><br /> FILTER<br /><br /> 封鎖|  
|operation (作業)|**int**|為述詞指定的作業類型：<br /><br /> Null = 所有適用的作業<br /><br /> 1 = 插入之後<br /><br /> 2 = 更新後<br /><br /> 3 = 更新之前<br /><br /> 4 = 刪除之前|  
|operation_desc|**nvarchar(60)**|為述詞指定的作業類型：<br /><br /> NULL<br /><br /> 插入之後<br /><br /> AFTER UPDATE<br /><br /> 更新之前<br /><br /> 刪除之前|  
  
## <a name="permissions"></a>權限  
 具有**ALTER ANY SECURITY POLICY**許可權的主體可存取此目錄檢視中的所有物件，以及具有物件之**view DEFINITION**的任何人。  
  
## <a name="see-also"></a>另請參閱  
 [資料列層級安全性](../../relational-databases/security/row-level-security.md)   
 [security_policies &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [&#40;Transact-sql&#41;建立安全性原則](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [&#40;Transact-sql&#41;的安全性目錄檢視](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
