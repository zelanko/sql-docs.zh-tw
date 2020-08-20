---
description: sysarticlecolumns (系統檢視) (Transact-SQL)
title: sysarticlecolumns (System View)  (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1a6e359aa7f6c0e7efc4090152b152ab1bfb6fbc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460266"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns (系統檢視) (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysarticlecolumns** view 會公開已發行之發行項中資料行的其他相關資訊。 這份檢視儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**>artid**|**int**|識別發行項。|  
|**colid**|**int**|識別發行項中的資料行。|  
|**is_udt**|**int**|指出資料行是否為使用者自訂資料類型 (UDT) 資料行。 值為 **1** 表示 UDT 資料行。|  
|**is_xml**|**int**|如果資料行是 **xml** 資料行，則為。 值為 **1** 表示 **xml** 資料行。|  
|**is_max**|**int**|這是指資料行是否為大數值資料類型資料行 (**Varchar (max) **、 **Nvarchar (max **) 或 **Varbinary (max) **) 。 值為 **1** 表示大型值資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [sp_articlecolumn &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
