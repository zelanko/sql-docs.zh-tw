---
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: c8d97513694a8f1b0559dbd029a6f9f3bed91cf5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver8712"></a>MSSQLSERVER_8712
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|8712|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|USEPLAN_ERR_NO_INDEX|  
|訊息文字|USE PLAN 提示中指定的索引 '%.*ls' 不存在。 請指定現有的索引，或用指定的名稱建立索引。|  
  
## <a name="explanation"></a>說明  
在 USE PLAN 提示中指定的索引不存在。  
  
## <a name="user-action"></a>使用者動作  
請確定在 USE PLAN 提示中指定的所有索引都存在。  
  
## <a name="see-also"></a>另請參閱  
[查詢提示 &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
  
