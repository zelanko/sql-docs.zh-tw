---
title: dbo.server_quotas (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: ''
ms.reviewer: ''
ms.prod_service: sql-database
ms.technology: system-objects
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
ms.openlocfilehash: e11b4ef7224a622b22c3d7cc15d97175c73625bd
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51671328"
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
  
  
