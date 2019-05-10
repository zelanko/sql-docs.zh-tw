---
title: sys.fulltext_document_types & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_document_types_TSQL
- fulltext_document_types
- fulltext_document_types_TSQL
- sys.fulltext_document_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_document_types catalog view
ms.assetid: 156fcfa4-7304-4a5c-b96f-1c3e061e5df0
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c11c21844b0709cf795375c4b8d17ee43847d06f
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/30/2019
ms.locfileid: "64945589"
---
# <a name="sysfulltextdocumenttypes-transact-sql"></a>sys.fulltext_document_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對可用於全文檢索索引作業的每一種文件類型，各傳回一個資料列。 每一個資料列都代表在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中註冊的 IFilter 介面。  
  
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**document_type**|**sysname**|支援之文件類型的副檔名。<br /><br /> 這個值可以用來找出將會用於全文檢索索引類型的資料行的篩選器**varbinary （max)** 或是**映像**。|  
|**class_id**|**uniqueidentifier**|支援副檔名之 IFilter 類別的 GUID。|  
|**path**|**nvarchar(260)**|通往 IFilter DLL 的路徑。 路徑，只會顯示的成員**serveradmin**固定的伺服器角色。|  
|**version**|**sysname**|IFilter DLL 的版本。|  
|**manufacturer**|**sysname**|IFilter 製造廠的名稱。<br /><br /> 注意:只記載為製造商[!INCLUDE[msCoName](../../includes/msconame-md.md)]上支援[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
