---
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0896f3e70e6c65a1fcd0de4169249fb622e6b5f8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85051081"
---
# <a name="localdb_error_too_many_shared_instances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|287|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|共用的執行個體太多，無法產生唯一的使用者執行個體名稱。 請取消共用部分現有的共用執行個體。|  
  
## <a name="explanation"></a>說明  
 共用的執行個體太多，無法產生唯一的使用者執行個體名稱。  
  
## <a name="user-action"></a>使用者動作  
 請取消共用一個或多個共用的本機資料庫執行階段執行個體，然後再試一次。  
  
  
