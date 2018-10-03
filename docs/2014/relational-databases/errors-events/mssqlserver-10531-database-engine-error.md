---
title: MSSQLSERVER_10531 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7324979238eda7f3ee63a709c199878350edb82d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48093948"
---
# <a name="mssqlserver10531"></a>MSSQLSERVER_10531
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
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
 [計畫指南](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
