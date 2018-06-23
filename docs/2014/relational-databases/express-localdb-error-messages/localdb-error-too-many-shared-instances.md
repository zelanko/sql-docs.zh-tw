---
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 865b682ec0f2a55d76ac9163da575aa5cbdaf9a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034999"
---
# <a name="localdberrortoomanysharedinstances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|287|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|共用的執行個體太多，無法產生唯一的使用者執行個體名稱。 請取消共用部分現有的共用執行個體。|  
  
## <a name="explanation"></a>說明  
 共用的執行個體太多，無法產生唯一的使用者執行個體名稱。  
  
## <a name="user-action"></a>使用者動作  
 請取消共用一個或多個共用的本機資料庫執行階段執行個體，然後再試一次。  
  
  