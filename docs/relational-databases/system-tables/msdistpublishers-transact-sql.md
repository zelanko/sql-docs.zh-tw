---
title: Msdb.dbo.msdistpublishers （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c19f2d8e75a3c9744318d65683b29d1d84857ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907418"
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  **Msdb.dbo.msdistpublishers**資料表會針對本機散發者所支援的每個遠端發行者，各包含一個資料列。 此資料表會儲存在**msdb**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|發行集散發者的名稱。|  
|**distribution_db**|**sysname**|散發資料庫的名稱。|  
|**working_directory**|**nvarchar(255)**|用來儲存發行集資料和結構描述檔案的工作目錄名稱。|  
|**security_mode**|**int**|在散發者端實作的安全性模式：<br /><br /> ****  =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。<br /><br /> **1** = Windows 驗證。|  
|**登入**|**sysname**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**許可權**|**Nvarchar （524）**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (加密)。|  
|**主動**|**bit**|指出本機散發者是否正由遠端發行者所使用。|  
|**trusted**|**bit**|指出遠端發行者所用的密碼，是否與本機散發者一樣：<br /><br /> **0** = 遠端發行者需要有密碼，才能連接到散發者。<br /><br /> **1** = 不需要密碼。|  
|**third_party**|**bit**|發行者是否為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一項安裝：<br /><br /> ****  =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝。**1** = 異質資料源。|  
|**publisher_type**|**sysname**|發行者類型：<br /><br /> ****  =  MSSQLSERVER[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。<br /><br /> **Oracle** = 標準的 oracle 發行者。<br /><br /> **ORACLE 閘道**= Oracle 閘道發行者。|  
|**storage_connection_string**|**Nvarchar （779）**|Azure SQL Database 儲存體連接字串的值。|  

  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
