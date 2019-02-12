---
title: dbo.server_quotas (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 657376be08e4cd404ce53d78114604cdd11fbda2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034439"
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **重要！！** 這適用於 **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 只 ！**  
>   
>  這項功能處於預覽狀態。 不要採用此功能的特定實作的相依性，因為在未來的版本中可能會變更或移除此功能。  
  
 傳回伺服器上可用的資料庫配額類型。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|伺服器的配額類型。 型別**Premium_database**就相當於與含有資源保留資料庫。|  
|quota_value|**int**|伺服器中允許的配額類型數目。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視可供所有使用者角色權限來連接到虛擬**主要**資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [管理高階資料庫](https://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
