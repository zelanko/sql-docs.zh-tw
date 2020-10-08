---
description: sys.database_usage (Azure SQL Database)
title: sys.database_usage (Azure SQL Database) Microsoft Docs
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
ms.openlocfilehash: f0c8809138bfad5cc9b7c4866978e7f2c111e09a
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809205"
---
# <a name="sysdatabase_usage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  **注意：這只適用于 Azure SQL Database V11。**  
  
 列出伺服器上資料庫的數目、類型和持續時間 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。  
  
 **Sys.database_usage** view 包含下列資料行。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|time|使用事件發生的日期。|  
|sku|資料庫的服務層類型： **Web**、 **Business**、 **Basic**、 **Standard**、 **Premium**|  
|quantity|當天存在之 SKU 類型資料庫的數目上限。|  
  
## <a name="permissions"></a>權限  
 此視圖的唯讀存取權可供具有連接 **master** 資料庫之許可權的所有使用者使用。  
  
## <a name="remarks"></a>備註  
 **Sys.database_usage** view 會針對您的訂用帳戶的每一天，各傳回一個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Database 定價詳細資料](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Azure SQL Database 中的帳戶和計費](/previous-versions/azure/ee621788(v=azure.100))  
  
