---
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: befd62e1875811092917445068689ed9cb3be62b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|611|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|VAR_SIZE_TOO_BIG|  
|訊息文字|無法插入或更新資料列，因為變數資料行的總大小 (包括負擔) 要比限制多出 %d 個位元組。|  
  
## <a name="explanation"></a>說明  
變數資料行大小上限多於結構描述允許的值。 當變數資料行大小超出啟用 Vardecimal 資料格式時固定案例中的限制，或是變數資料行大小超出 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 壓縮資料記錄所允許的限制時，就會傳回錯誤 611。  
  
## <a name="user-action"></a>使用者動作  
縮減此記錄的大小。  
  
