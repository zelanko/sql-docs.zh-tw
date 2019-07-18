---
title: sys.database_usage (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- database_usage
- database_usage_TSQL
- sys.database_usage_TSQL
- sys.database_usage
dev_langs:
- TSQL
helpviewer_keywords:
- database_usage
- sys.database_usage
ms.assetid: be6820de-60bf-4ddd-ace7-4077893d630f
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d64f3e03db3eaf12755eb36d41814d4548a2ae52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079404"
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **注意：只適用於 Azure SQL Database V11。**  
  
 列出數目、 類型和持續時間的資料庫上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]伺服器。  
  
 **Sys.database_usage**檢視包含下列資料行。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|time|使用事件發生的日期。|  
|sku|資料庫服務層的類型：**Web**，**商務**，**基本**，**標準**， **Premium**|  
|quantity|當天存在之 SKU 類型資料庫的數目上限。|  
  
## <a name="permissions"></a>Permissions  
 唯讀存取此檢視會提供給有權連接到的所有使用者**主要**資料庫。  
  
## <a name="remarks"></a>備註  
 **Sys.database_usage**檢視會傳回一個資料列，每一天的訂用帳戶。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Database 定價詳細資料](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [帳戶和 Windows Azure SQL Database 中的計費](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
