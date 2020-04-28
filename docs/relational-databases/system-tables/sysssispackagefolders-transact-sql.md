---
title: sysssispackagefolders （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: d2ff4537f5db246dd9bcdc114b02005402f8745f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029606"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對所使用之資料夾階層中的每個邏輯資料夾[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，各包含一個資料列。 當您連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的物件總管會列出這些資料夾。 資料夾會列出儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或檔案系統中的封裝。  
  
 **Parentfolderid**資料行描述資料夾階層。 資料夾階層頂端的資料夾包含**parentfolderid**中的 null 值。  
  
 [**資料夾**名稱] 資料行包含物件總管中顯示的資料夾名稱。  
  
 此資料表會儲存在**msdb**資料庫中。  

  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|資料夾的 GUID。|  
|**parentfolderid**|**uniqueidentifier**|本身是父資料夾之資料夾的 GUID。|  
|**名**|**sysname**|資料夾的名稱。 這個名稱會出現在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的資料夾階層中。|  
  
  
