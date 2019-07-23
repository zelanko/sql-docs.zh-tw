---
title: MSSQLSERVER_10531 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f9f7eaf086b3209dd5697bcf227a834ebe7cb916
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068137"
---
# <a name="mssqlserver10531"></a>MSSQLSERVER_10531
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10531|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_NO_ELIGIBLE_STMT|  
|訊息文字|無法從快取建立計畫指南 '%.*ls'，因為使用者沒有所需的權限。 請將 VIEW SERVER STATE 權限授予建立計畫指南的使用者。|  
  
## <a name="explanation"></a>說明  
使用者沒有足夠的權限，無法從計畫快取建立指定的計畫指南。  
  
## <a name="user-action"></a>使用者動作  
請將 VIEW SERVER STATE 權限授予建立計畫指南的使用者。  
  
## <a name="see-also"></a>另請參閱  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
