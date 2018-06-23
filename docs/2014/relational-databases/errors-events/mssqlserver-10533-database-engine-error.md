---
title: MSSQLSERVER_10533 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 458716b859df07b3bef456a1c2e515168fc10744
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132885"
---
# <a name="mssqlserver10533"></a>MSSQLSERVER_10533
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
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
 [計畫指南](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
