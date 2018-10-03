---
title: sysarticlecolumns （系統檢視） (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: f5e5deebbfc386b84cbac8dbff28b057b152278d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762026"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns (系統檢視) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysarticlecolumns**檢視會顯示有關已發行的文章中的資料行的其他資訊。 這份檢視儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**artid&lt**|**int**|識別發行項。|  
|**colid**|**int**|識別發行項中的資料行。|  
|**is_udt**|**int**|指出資料行是否為使用者自訂資料類型 (UDT) 資料行。 值為**1**表示 UDT 資料行。|  
|**is_xml**|**int**|是資料行是否**xml**資料行。 值為**1**指出**xml**資料行。|  
|**is_max**|**int**|是資料行是否為大數值資料類型資料行 (**varchar （max)**， **nvarchar （max)** 或是**varbinary （max)**)。 值為**1**表示大數值資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
