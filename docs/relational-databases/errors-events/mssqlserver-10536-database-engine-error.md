---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c5e9c4574c462ef42b0235e843970c882532dc56
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635376"
---
# <a name="mssqlserver10536"></a>MSSQLSERVER_10536
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|10536|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_TOO_MANY_STMTS|  
|訊息文字|無法建立計畫指南 '%.\*ls'，因為指定的 **@plan_handle** 所對應的批次或模組中包含超過 1000 個適合的陳述式。 請為批次或模組中的每個陳述式分別指定 **statement_start_offset** 值，以各建立一個計畫指南。|  
  
## <a name="explanation"></a>說明  
指定的 **@plan_handle** 所對應的批次或模組中包含超過 1000 個適合的陳述式。  
  
## <a name="user-action"></a>使用者動作  
請為批次或模組中的每個陳述式分別指定 **statement_start_offset** 值，以各建立一個計畫指南。  
  
## <a name="see-also"></a>另請參閱  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
