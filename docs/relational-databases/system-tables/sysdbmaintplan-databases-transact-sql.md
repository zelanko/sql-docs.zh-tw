---
title: sysdbmaintplan_databases (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_databases
- sysdbmaintplan_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_databases system table
ms.assetid: f8413a44-8fcc-4899-84f2-b4afe0f8ec08
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 890fa10c306ac35e8a72ed3427bedeeead82401c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33256574"
---
# <a name="sysdbmaintplandatabases-transact-sql"></a>sysdbmaintplan_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此資料表是以保留現有的資訊，針對從已升級的執行個體的先前版本[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本都不會變更此資料表的內容。 這份資料表儲存在**msdb**資料庫。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**Uniqueidentifier**|維護計畫識別碼。|  
|**database_name**|**sysname**|資料庫維護計畫之相關資料庫的名稱。|  
  
  
