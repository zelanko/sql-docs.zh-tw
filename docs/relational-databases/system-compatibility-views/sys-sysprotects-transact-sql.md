---
title: "sys.sysprotects (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysprotects
- sys.sysprotects_TSQL
- sys.sysprotects
- sysprotects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprotects compatibility view
- sysprotects system table
ms.assetid: 49c9658d-fb51-4c77-94a0-fba699b0102d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: abde43e1d699c32b2a9cd21459d823692952e059
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="syssysprotects-transact-sql"></a>sys.sysprotects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含利用 GRANT 和 DENY 陳述式，套用至資料庫中安全性帳戶之權限的相關資訊。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|這些權限所要套用至的物件識別碼。|  
|**uid**|**smallint**|這些權限所要套用至的使用者或群組識別碼。 如果使用者和角色數目超過 32,767 個，則會造成溢位或傳回 NULL。|  
|**action**|**tinyint**|可以有下列權限之一：<br /><br /> 26 = REFERENCES <br /><br /> 178 = CREATE FUNCTION <br /><br /> 193 = SELECT <br /><br /> 195 = INSERT<br /><br /> 196 = DELETE<br /><br /> 197 = 更新<br /><br /> 198 = CREATE TABLE <br /><br /> 203 = CREATE DATABASE <br /><br /> 207 = CREATE VIEW <br /><br /> 222 = CREATE PROCEDURE <br /><br /> 224 = EXECUTE <br /><br /> 228 = BACKUP DATABASE <br /><br /> 233 = CREATE DEFAULT <br /><br /> 235 = BACKUP LOG <br /><br /> 236 = CREATE RULE|  
|**protecttype**|**tinyint**|其值如下：<br /><br /> 204 = GRANT_W_GRANT <br /><br /> 205 = GRANT <br /><br /> 206 = DENY|  
|**columns**|**varbinary(8000)**|這些 SELECT 或 UPDATE 權限所要套用至的資料行之點陣圖。<br /><br /> Bit 0 = 所有的資料行。<br /><br /> Bit 1 = 將權限套用至該資料行。<br /><br /> NULL = 沒有資訊。|  
|**grantor**|**smallint**|發出 GRANT 或 DENY 權限之使用者的使用者識別碼。 如果使用者和角色數目超過 32,767 個，則會造成溢位或傳回 NULL。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
