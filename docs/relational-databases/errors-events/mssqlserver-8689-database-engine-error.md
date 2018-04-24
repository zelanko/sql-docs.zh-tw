---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2fd9de9054caa1f6c0287774f1dc12b5a663fe4f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver8689"></a>MSSQLSERVER_8689
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|8689|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|USEPLAN_ERR_NO_DB|  
|訊息文字|USE PLAN 提示中指定的資料庫 '%.*ls' 不存在。 請指定現有的資料庫。|  
  
## <a name="explanation"></a>說明  
在 USE PLAN 提示中指定的資料庫不存在。  
  
## <a name="user-action"></a>使用者動作  
請確定在 USE PLAN 提示中指定的所有資料庫都存在。  
  
## <a name="see-also"></a>另請參閱  
[查詢提示 &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
  
