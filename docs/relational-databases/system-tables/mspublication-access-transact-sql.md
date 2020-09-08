---
description: MSpublication_access (Transact-SQL)
title: MSpublication_access (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublication_access_TSQL
- MSpublication_access
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublication_access system table
ms.assetid: 7bebe47e-3153-4579-8092-5723667a24c6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f8a6e52f94bae4214c1a40e1f180c73b0193c5ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89524595"
---
# <a name="mspublication_access-transact-sql"></a>MSpublication_access (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSpublication_access**資料表針對每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可存取特定發行集或發行者的登入，各包含一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|發行集的識別碼。|  
|**登錄**|**sysname**|存在於發行者和散發者端的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
