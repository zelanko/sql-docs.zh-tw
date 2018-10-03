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
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5166d82d0212c3974cbc7f95b071765ef25afdb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740586"
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
|**資料夾名稱**|**sysname**|資料夾的名稱。 這個名稱會出現在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的資料夾階層中。|  
  
  
