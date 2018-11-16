---
title: sys.database_usage (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f17e34de7c230b111652ea57a3baa072a442a6a5
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656737"
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **注意： 這只適用於 Azure SQL Database V11。**  
  
 列出數目、 類型和持續時間的資料庫上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]伺服器。  
  
 **Sys.database_usage**檢視包含下列資料行。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|time|使用事件發生的日期。|  
|sku|資料庫服務層的類型： **Web**，**商務**，**基本**，**標準**， **Premium**|  
|quantity|當天存在之 SKU 類型資料庫的數目上限。|  
  
## <a name="permissions"></a>Permissions  
 唯讀存取此檢視會提供給有權連接到的所有使用者**主要**資料庫。  
  
## <a name="remarks"></a>備註  
 **Sys.database_usage**檢視會傳回一個資料列，每一天的訂用帳戶。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Database 定價詳細資料](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [帳戶和 Windows Azure SQL Database 中的計費](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
