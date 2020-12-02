---
description: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
title: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 35b4d6fa-ebb9-49d3-aaab-d4e37b6f3760
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 4e4b290daa5dee2fb2a7cc5d3d608b81a7eae438
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506262"
---
# <a name="localdb_error_instance_already_shared"></a>LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |
| --------- | ----- |
|產品名稱|SQL Server|  
|事件識別碼|284|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|已共用指定的本機資料庫執行個體。|  
  
## <a name="explanation"></a>說明  
 指定的本機資料庫執行個體已用其他共用名稱共用。  
  
## <a name="user-action"></a>使用者動作  
 請先取消共用已共用的執行個體，然後再次使用不同的共用名稱來共用它。  
  
  
