---
title: "sys.securable_classes (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- securable_classes_TSQL
- securable_classes
- sys.securable_classes_TSQL
- sys.securable_classes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.securable_classes catalog view
ms.assetid: ae2bf589-17be-4cad-b5d5-05a34173b32d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d21b559f232a05ab8699962b4691aa3b4e3bea9
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="syssecurableclasses-transact-sql"></a>sys.securable_classes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回安全性實體類別的清單  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**class_desc**|**sysname**|類別的名稱。|  
|**class**|**int**|類別的數值指定。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所支援的安全性實體類別。  
  
```sql  
SELECT * FROM sys.securable_classes ORDER BY class;  
```  
  
## <a name="see-also"></a>請參閱  
 [安全性實體](../../relational-databases/security/securables.md)  
  
  
