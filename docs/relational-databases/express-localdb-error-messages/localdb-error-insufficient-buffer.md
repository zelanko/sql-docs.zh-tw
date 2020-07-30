---
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
author: stevestein
ms.author: sstein
ms.openlocfilehash: cdb7c78a8301ec11ddd54329c4c68943ea66afd2
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245190"
---
# <a name="localdb_error_insufficient_buffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |
| --------- | ----- |
|產品名稱|SQL Server|  
|事件識別碼|276|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|傳遞至本機資料庫執行個體 API 方法的緩衝區之大小不足。|  
  
## <a name="explanation"></a>說明  
 輸入緩衝區太短，且未要求截斷。  
  
## <a name="user-action"></a>使用者動作  
 請提供指定大小的緩衝區。  
  
  
