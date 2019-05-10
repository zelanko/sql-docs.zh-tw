---
title: sysssispackagefolders (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2604fa585bc7b27fc385336e1af71079efb68404
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489780"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含每個邏輯資料夾的資料夾階層中的一個資料列， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]使用。 當您連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的物件總管會列出這些資料夾。 資料夾會列出儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或檔案系統中的封裝。  
  
 **Parentfolderid**資料行描述資料夾階層。 在資料夾階層頂端的資料夾包含 null 值在**parentfolderid**。  
  
 **Foldername**資料行包含出現在 [物件總管] 中的資料夾名稱。  
  
 這份資料表儲存在**msdb**資料庫。  

  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|資料夾的 GUID。|  
|**parentfolderid**|**uniqueidentifier**|本身是父資料夾之資料夾的 GUID。|  
|**foldername**|**sysname**|資料夾的名稱。 這個名稱會出現在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的資料夾階層中。|  
  
  
