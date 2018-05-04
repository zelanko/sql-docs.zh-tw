---
title: sys.database_usage （SQL Azure 資料庫） |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 7754ed63cc6325b9b6cf1650e7b71daad03393ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **注意： 這只適用於 Azure SQL Database V11。**  
  
 列出數目、 類型和持續時間的資料庫上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]伺服器。  
  
 **Sys.database_usage**檢視包含下列資料行。  
  
|資料行名稱|Description|  
|-----------------|-----------------|  
|time|使用事件發生的日期。|  
|sku|為資料庫服務層的類型： **Web**，**商務**，**基本**，**標準**， **Premium**|  
|quantity|當天存在之 SKU 類型資料庫的數目上限。|  
  
## <a name="permissions"></a>Permissions  
 此檢視的唯讀存取可供所有使用者有權連接到**主要**資料庫。  
  
## <a name="remarks"></a>備註  
 **Sys.database_usage**檢視您的訂用帳戶的每一天傳回一個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Database 定價詳細資料](http://go.microsoft.com/fwlink/?LinkID=394978)   
 [帳戶和 Windows Azure SQL Database 中的計費](http://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
