---
title: sys.remote_service_bindings (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.remote_service_bindings_TSQL
- remote_service_bindings_TSQL
- remote_service_bindings
- sys.remote_service_bindings
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_service_bindings catalog view
ms.assetid: 4e1a885d-eed1-4993-9c87-e6fd781f437d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c326a5dd3a964209af0cc4834b91bca9071da9e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904587"
---
# <a name="sysremoteservicebindings-transact-sql"></a>sys.remote_service_bindings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這份目錄檢視針對每一個遠端服務繫結，各包含一個資料列。 
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|這個遠端服務繫結的名稱。 不是 NULLABLE。|  
|**remote_service_binding_id**|**int**|這個遠端服務繫結的識別碼。 不是 NULLABLE。|  
|**principal_id**|**int**|擁有這個遠端服務繫結的資料庫主體識別碼。 NULLABLE。|  
|**remote_service_name**|**nvarchar(256)**|這個繫結所套用的遠端服務名稱。 NULLABLE。|  
|**service_contract_id**|**int**|這個繫結所套用的合約識別碼。 0 值代表萬用字元，表示這個繫結適用於該服務所有的合約。 不是 NULLABLE。|  
|**remote_principal_id**|**int**|在遠端服務繫結所指定的使用者識別碼。 Service Broker 是採用這個使用者所擁有的憑證，與指定合約上的指定服務通訊。 NULLABLE。|  
|**is_anonymous_on**|**bit**|這個遠端服務繫結使用 ANONYMOUS 安全性。 開始交談的使用者身分，不會提供給目標服務。 不是 NULLABLE。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
