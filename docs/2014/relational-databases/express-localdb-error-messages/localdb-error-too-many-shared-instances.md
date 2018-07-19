---
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ffd2b6605189e58a6fc9324e9ef8b9caaf961e6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425687"
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
  
  
