---
title: MSSQLSERVER_10534 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 153227c6d24d6c73e89f09820110b514192c2736
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10534"></a>MSSQLSERVER_10534
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10534|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_INVALID_PARAMS|  
|訊息文字|無法建立計畫指南 '%.\*ls'，因為指定的 **@params** 值無效。 請以 *parameter_name parameter_type* 格式指定值，或指定 NULL。|  
  
## <a name="explanation"></a>說明  
針對 **@params** 指定的值無效。  
  
## <a name="user-action"></a>使用者動作  
請以 *parameter_name parameter_type* 格式指定值，或指定 NULL。  
  
## <a name="see-also"></a>另請參閱  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
