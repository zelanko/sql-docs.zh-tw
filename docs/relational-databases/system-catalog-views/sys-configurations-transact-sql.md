---
title: sys.configurations & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9eb9ced4e010001f42e106ce8b1903e029f2f1c4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109562"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對系統中每個伺服器範圍組態選項值，各包含一個資料列。  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|組態值的唯一識別碼。|  
|**name**|**nvarchar(35)**|組態選項的名稱。|  
|**value**|**sql_variant**|針對這個選項所設定的值。|  
|**minimum**|**sql_variant**|組態選項的最小值。|  
|**maximum**|**sql_variant**|組態選項的最大值。|  
|**value_in_use**|**sql_variant**|這個選項目前有效的執行值。|  
|**description**|**nvarchar(255)**|組態選項的描述。|  
|**is_dynamic**|**bit**|1 = 在執行 RECONFIGURE 陳述式時的有效變數。|  
|**is_advanced**|**bit**|1 = 會顯示變數時，才**顯示 advancedoption**設定。|  
  
 如需所有伺服器組態選項的清單，請參閱 <<c0> [ 伺服器組態選項&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。</c0>  
  
> [!NOTE]  
>  如需資料庫層級組態選項，請參閱[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 若要設定軟體 NUMA，請參閱[NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器範圍組態目錄檢視&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
