---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8b4444dc2ed1b239670c75321ec3a0e1401122a0
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|MSSQLSERVER|  
|事件識別碼|8710|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|訊息文字|必須提供搭配 CUBE、ROLLUP 或 GROUPING SET 查詢使用的彙總函式才能進行合併子彙總。 如果要修正這個問題，請移除彙總函式或在 GROUP BY 子句之上使用 UNION ALL 來撰寫查詢。|  
  
## <a name="explanation"></a>說明  
已搭配 CUBE、ROLLUP 或 GROUPING SETS 使用的彙總函式未提供合併子彙總的方法。  
  
## <a name="user-action"></a>使用者動作  
如果要修正這個問題，請移除彙總函式或在 GROUP BY 子句之上使用 UNION ALL 來撰寫查詢。  
  

