---
description: dbo.syscategories (Transact-SQL)
title: dbo.sys分類 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 84d72b2ec08573b7c7aa72903eab1bc828d6f774
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525118"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  包含 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 用來組織作業、警示和運算子的類別目錄。 此資料表儲存在 **msdb** 資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|類別目錄識別碼|  
|**category_class**|**int**|類別目錄中的項目類型：<br /><br /> **1** = 作業<br /><br /> **2** = 警示<br /><br /> **3** = 運算子|  
|**category_type**|**tinyint**|類別目錄類型：<br /><br /> **1** = 本機<br /><br /> **2** = 多伺服器<br /><br /> **3** = 無|  
|**name**|**sysname**|類別目錄的名稱|  
  
  
