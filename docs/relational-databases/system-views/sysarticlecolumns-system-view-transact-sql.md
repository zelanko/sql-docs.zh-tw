---
title: sysarticlecolumns （系統檢視）（Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 84d528cf252c30da580f36539b6ea665c056a047
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889144"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns (系統檢視) (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysarticlecolumns** view 會公開已發行之文章中資料行的其他相關資訊。 這份檢視儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|識別發行項。|  
|**colid**|**int**|識別發行項中的資料行。|  
|**is_udt**|**int**|指出資料行是否為使用者自訂資料類型 (UDT) 資料行。 值為**1**表示 UDT 資料行。|  
|**is_xml**|**int**|這是指資料行是否為**xml**資料行。 值為**1**表示**xml**資料行。|  
|**is_max**|**int**|這是指資料行是否為大數值資料類型資料行（**Varchar （max）**、 **Nvarchar （max）** 或**Varbinary （max）**）。 值為**1**表示大數值資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [sp_articlecolumn &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
