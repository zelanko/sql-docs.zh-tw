---
title: MSSQLSERVER_10502 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33bb9c3e6bc3e3f1d198be344832451eafe9b22c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68095676"
---
# <a name="mssqlserver_10502"></a>MSSQLSERVER_10502
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10502|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_DUP_FOUND|  
|訊息文字|無法建立計畫指南 '%.*ls'，因為 @stmt 和 @module_or_batch 或是 @plan_handle 和 @statement_start_offset 所指定的陳述式與資料庫中現有的計畫指南 '%.\*ls' 相符。 請卸除現有計畫指南後，再建立新的計畫指南。|  
  
## <a name="explanation"></a>說明  
指定之陳述式的計畫指南已存在。  
  
## <a name="user-action"></a>使用者動作  
請卸除現有計畫指南後，再建立新的計畫指南。  
  
## <a name="see-also"></a>另請參閱  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
