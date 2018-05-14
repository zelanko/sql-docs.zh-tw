---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 28b8eb71cc0e50925788596d1b23572a51064423
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
