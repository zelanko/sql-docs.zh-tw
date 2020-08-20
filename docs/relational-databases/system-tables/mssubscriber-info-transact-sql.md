---
description: MSsubscriber_info (Transact-SQL)
title: MSsubscriber_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_info_TSQL
- MSsubscriber_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_info system table
ms.assetid: 5ca22f41-6020-4f72-8110-e69baf3447cb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5b807bcb3595a20bcce849b6526e9729c960d5bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480728"
---
# <a name="mssubscriber_info-transact-sql"></a>MSsubscriber_info (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSsubscriber_info**資料表針對正在從本機散發者發送訂閱的每個發行者/訂閱者配對，各包含一個資料列。 這份資料表儲存在散發資料庫中。  
  
 **注意** 這個系統資料表已被取代，並維持在支援舊版的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="definition"></a>定義  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|發行者的名稱。|  
|**使用者**|**sysname**|訂閱者的名稱。|  
|**type**|**tinyint**|訂閱者類型：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。<br /><br /> **1** = ODBC 資料來源。|  
|**登錄**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入。 如果利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證模式來加入訂閱者，便以加密格式來儲存。|  
|**password**|**Nvarchar (524) **|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼。 如果利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證模式來加入訂閱者，便以加密格式來儲存。|  
|**description**|**nvarchar(255)**|訂閱者的描述。|  
|**security_mode**|**int**|實作的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。<br /><br /> **1**個  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
