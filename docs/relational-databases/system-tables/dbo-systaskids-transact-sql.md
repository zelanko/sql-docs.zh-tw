---
title: dbo.systaskids (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- systaskids_TSQL
- dbo.systaskids
- systaskids
- dbo.systaskids_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systaskids system table
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9ed9ac8e81abaf6367d3a9c5518f1f18cb94ef8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990405"
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所建立的工作與目前版本中 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 作業的對應。 這份資料表儲存在**msdb**資料庫。  
  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|工作識別碼|  
|**job_id**|**uniqueidentifier**|工作所對應之作業的識別碼|  
  
  
