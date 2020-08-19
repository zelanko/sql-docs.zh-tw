---
description: sysssispackagefolders (Transact-SQL)
title: sysssispackagefolders (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 7924de782ca499f5a92458d0024b57877c7310c0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419122"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對資料夾階層中使用的每個邏輯資料夾，各包含一個資料列 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。 當您連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的物件總管會列出這些資料夾。 資料夾會列出儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或檔案系統中的封裝。  
  
 **Parentfolderid**資料行描述資料夾階層。 資料夾階層頂端的資料夾在 **parentfolderid**中包含 null 值。  
  
 [ **資料夾** 名稱] 資料行包含出現在物件總管中的資料夾名稱。  
  
 此資料表儲存在 **msdb** 資料庫中。  

  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|資料夾的 GUID。|  
|**parentfolderid**|**uniqueidentifier**|本身是父資料夾之資料夾的 GUID。|  
|**名**|**sysname**|資料夾的名稱。 這個名稱會出現在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的資料夾階層中。|  
  
  
