---
title: MSSQLSERVER_8712 | Microsoft Docs
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
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6231e5d0aac503b257657130a2fecb4fa9699375
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver8712"></a>MSSQLSERVER_8712
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
