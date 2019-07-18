---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 79c9fc7c9c15d83dafc8d117e142fc06741c11ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912493"
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
  
  
