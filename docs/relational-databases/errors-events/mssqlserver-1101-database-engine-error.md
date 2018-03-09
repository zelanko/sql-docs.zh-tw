---
title: MSSQLSERVER_1101 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e99a6a8072f882f794f2406c66c6b0625cbc7d4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1101"></a>MSSQLSERVER_1101
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1101|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NOALLOCPG|  
|訊息文字|檔案群組中的磁碟空間不足，無法為資料庫 '%.*ls' 配置新的頁面，檔案群組：'%.\*ls'。 請卸除檔案群組中的物件、將其他檔案加入檔案群組，或將檔案群組中現有檔案設定為自動成長，以產生必要的空間。|  
  
## <a name="explanation"></a>說明  
檔案群組中沒有可用的磁碟空間。  
  
## <a name="user-action"></a>使用者動作  
下列動作可以在檔案群組中提供可用的空間。  
  
-   開啟自動成長功能。  
  
-   加入更多檔案到檔案中。  
  
-   卸除檔案群組中不需要的索引或資料表，以釋出磁碟空間。  
  
