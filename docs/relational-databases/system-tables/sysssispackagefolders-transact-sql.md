---
title: sysssispackagefolders (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
caps.latest.revision: 22
author: douglasl
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 179e6c1241ccbe42528eae591696727c9cea541a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含每個邏輯資料夾的資料夾階層中的一個資料列， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]使用。 當您連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的物件總管會列出這些資料夾。 資料夾會列出儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或檔案系統中的封裝。  
  
 **Parentfolderid**資料行描述資料夾階層。 在資料夾階層最上方的資料夾包含中的 null 值**parentfolderid**。  
  
 **Foldername**資料行包含出現在 [物件總管] 中的資料夾名稱。  
  
 這份資料表儲存在**msdb**資料庫。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|資料夾的 GUID。|  
|**parentfolderid**|**uniqueidentifier**|本身是父資料夾之資料夾的 GUID。|  
|**資料夾名稱**|**sysname**|資料夾的名稱。 這個名稱會出現在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的資料夾階層中。|  
  
  
