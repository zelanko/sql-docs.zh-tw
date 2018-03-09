---
title: MSSQLSERVER_2538 | Microsoft Docs
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
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6b696097a4bfdec2e625de4523fc7689f230f6cc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2538"></a>MSSQLSERVER_2538
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2538|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|訊息文字|檔案 FILE。 範圍數目 = EXTENTS，使用的頁面 = USED_PAGES，保留的頁面 = RESERVED_PAGES。|  
  
## <a name="explanation"></a>說明  
這項資訊是 DBCC CHECKALLOC 命令輸出的一部分， 也是指定資料庫中已配置範圍、已使用頁面和已保留頁面的個別檔案摘要資訊。  
  
## <a name="user-action"></a>使用者動作  
無  
  
