---
title: "sys.parameter_type_usages (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.parameter_type_usages
- sys.parameter_type_usages_TSQL
- parameter_type_usages_TSQL
- parameter_type_usages
dev_langs: TSQL
helpviewer_keywords: sys.parameter_type_usages catalog view
ms.assetid: af0e167b-bffb-4525-84ec-3607f9268d3d
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e477f00a9f80159daa74bb3199c8629f52322b9b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysparametertypeusages-transact-sql"></a>sys.parameter_type_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個使用者自訂類型參數，各傳回一個資料列。  
  
> [!NOTE]  
>  這份檢視不會傳回編號程序的參數資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|這個參數所屬物件的識別碼。|  
|**parameter_id**|**int**|參數的識別碼。 在物件中，這是唯一的。|  
|**user_type_id**|**int**|使用者自訂類型的識別碼。<br /><br /> 若要傳回的型別名稱，加入[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目錄檢視這個資料行。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [純量類型目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
