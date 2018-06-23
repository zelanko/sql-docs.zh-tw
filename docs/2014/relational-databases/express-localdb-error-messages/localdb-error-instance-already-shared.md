---
title: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED |Microsoft 文件
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
ms.assetid: 35b4d6fa-ebb9-49d3-aaab-d4e37b6f3760
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2d0d59be487d0a54e821b4f27160f8dd124c9db8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135804"
---
# <a name="localdberrorinstancealreadyshared"></a>LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|284|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|已共用指定的本機資料庫執行個體。|  
  
## <a name="explanation"></a>說明  
 指定的本機資料庫執行個體已用其他共用名稱共用。  
  
## <a name="user-action"></a>使用者動作  
 請先取消共用已共用的執行個體，然後再次使用不同的共用名稱來共用它。  
  
  