---
description: MSSQLSERVER_10521
title: MSSQLSERVER_10521 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3c7b3bad98a125072b88e3a009c97d1011d8872c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338544"
---
# <a name="mssqlserver_10521"></a>MSSQLSERVER_10521
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|10521|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_PARAM_NEEDED|  
|訊息文字|無法建立計劃指南 '%.\*ls'，因為 **\@type** 已指定為 '%ls'，且參數 '%ls' 為 NULL。 但這種類型要求參數必須為非 NULL 值。 請為參數指定非 NULL 值，或將參數類型變更為允許 NULL 值的類型。|  
  
## <a name="explanation"></a>說明  
在 **\@type** 中指定的類型要求指定參數必須為非 NULL 值，但提供的卻是 NULL 值。  
  
## <a name="user-action"></a>使用者動作  
請為參數指定非 NULL 值，或將參數類型變更為允許 NULL 值的類型。  
  
## <a name="see-also"></a>另請參閱  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
