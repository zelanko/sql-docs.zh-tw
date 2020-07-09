---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b57f8a7985c9fb092209bc5a80b9d0c3294d98c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781498"
---
# <a name="mssqlserver_10519"></a>MSSQLSERVER_10519
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|10519|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|訊息文字|無法建立計畫指南 '%.\*ls'，因為無法將 **\@hints** 中指定的提示套用至 **\@stmt** 或 **\@statement_start_offset** 指定的陳述式。 請確認提示能否套用至陳述式。|  
  
## <a name="explanation"></a>說明  
無法將 **\@hints** 中指定的提示套用至 **\@stmt** 或 **\@statement_start_offset** 指定的陳述式。  
  
## <a name="user-action"></a>使用者動作  
請指定能夠套用至陳述式的提示。  
  
## <a name="see-also"></a>另請參閱  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
