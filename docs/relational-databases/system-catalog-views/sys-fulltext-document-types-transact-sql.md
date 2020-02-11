---
title: sys.databases fulltext_document_types （Transact-sql） |Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e60f977c220d14680499ca12a4884e912587b7b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68133845"
---
# <a name="sysfulltext_document_types-transact-sql"></a>sys.fulltext_document_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對可用於全文檢索索引作業的每一種文件類型，各傳回一個資料列。 每一個資料列都代表在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中註冊的 IFilter 介面。  
  
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**document_type**|**sysname**|支援之文件類型的副檔名。<br /><br /> 此值可用來識別將在**Varbinary （max）** 或**image**類型之資料行的全文檢索索引期間使用的篩選。|  
|**class_id**|**uniqueidentifier**|支援副檔名之 IFilter 類別的 GUID。|  
|**路徑名**|**nvarchar(260)**|通往 IFilter DLL 的路徑。 只有**serveradmin**固定伺服器角色的成員才看得到該路徑。|  
|**版本**|**sysname**|IFilter DLL 的版本。|  
|**manufacturer**|**sysname**|IFilter 製造廠的名稱。<br /><br /> 注意：僅支援隨附製造商[!INCLUDE[msCoName](../../includes/msconame-md.md)]的檔。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
