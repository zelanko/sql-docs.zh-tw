---
title: sys. database_usage （Azure SQL Database） |Microsoft Docs
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
ms.openlocfilehash: 0a0789ebd9a5aa4bd10605d69afa59a586ce75b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70155538"
---
# <a name="sysdatabase_usage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **注意：這僅適用于 Azure SQL Database V11。**  
  
 列出[!INCLUDE[ssSDS](../../includes/sssds-md.md)]伺服器上資料庫的數目、類型和持續時間。  
  
 [ **Sys.databases database_usage** ] 視圖包含下列資料行。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|time|使用事件發生的日期。|  
|sku|資料庫的服務層級類型： **Web**、 **Business**、 **Basic**、 **Standard**、 **Premium**|  
|quantity|當天存在之 SKU 類型資料庫的數目上限。|  
  
## <a name="permissions"></a>權限  
 此視圖的唯讀存取權可供所有具有連接到**master**資料庫之許可權的使用者使用。  
  
## <a name="remarks"></a>備註  
 **Database_usage** view 會針對訂閱的每一天傳回一個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Database 定價詳細資料](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Azure SQL Database 中的帳戶和計費](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
