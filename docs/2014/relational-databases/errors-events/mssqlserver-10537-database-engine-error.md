---
title: MSSQLSERVER_10537 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cf13b4b047a463979e012252013cccdc20b678d4
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554083"
---
# <a name="mssqlserver_10537"></a>MSSQLSERVER_10537
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10537|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_DUP_ENABLED|  
|訊息文字|無法啟用計畫指南 '%.*ls'，因為啟用的計畫指南 '%.\*ls' 中包含相同範圍和起始位移值的陳述式。 請停用現有的計畫指南後，再啟用指定的計畫指南。|  
  
## <a name="explanation"></a>說明  
 現有的計畫指南與指定之計畫指南中的陳述式包含相同範圍和起始位移值。  
  
## <a name="user-action"></a>使用者動作  
 請停用現有的計畫指南後，再啟用指定的計畫指南。  
  
## <a name="see-also"></a>另請參閱  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [計劃指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
