---
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b956a9f51e013ce03801ff870e27f337c738b3c6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62762060"
---
# <a name="mssqlserver8712"></a>MSSQLSERVER_8712
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
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
 [查詢提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [計畫指南](../performance/plan-guides.md)  
  
  
