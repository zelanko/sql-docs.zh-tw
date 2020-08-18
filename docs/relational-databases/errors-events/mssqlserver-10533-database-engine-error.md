---
description: MSSQLSERVER_10533
title: MSSQLSERVER_10533 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4ab2b32fab50f3a335d1d89fa76f0a3e26467e5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338894"
---
# <a name="mssqlserver_10533"></a>MSSQLSERVER_10533
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|10533|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_NAME_TOO_BIG|  
|訊息文字|無法建立計畫指南 '%.*ls'，因為計畫指南名稱超出允許的最大字元數 124 個字元。 請指定少於 125 個字元的名稱。|  
  
## <a name="explanation"></a>說明  
計畫指南名稱超出允許的最大字元數 124 個字元。  
  
## <a name="user-action"></a>使用者動作  
請指定少於 125 個字元的名稱。  
  
## <a name="see-also"></a>另請參閱  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
