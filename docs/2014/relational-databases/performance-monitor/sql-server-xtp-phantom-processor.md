---
title: XTP 虛設處理器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 14c34bb0d7520b914d8dbfc1cfc8174341722ece
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63150980"
---
# <a name="xtp-phantom-processor"></a>XTP 虛設處理器
  XTP 虛設處理器效能物件包含與 XTP 引擎的虛設處理子系統相關的計數器。 此元件負責偵測在 SERIALIZABLE 隔離等級執行之交易中的虛設項目列。  
  
 下表描述**XTP 虛設處理器**計數器。  
  
|計數器|描述|  
|-------------|-----------------|  
|**塵封角落掃描重試次數/秒 (由虛設項目發出)**|虛設處理器發出塵封角落掃掠期間，(平均) 每秒因為發生寫入衝突而進行掃描的重試次數。 這是層級非常低的計數器，非供客戶使用。|  
|**移除的虛設過期資料列/秒**|(平均) 每秒虛設掃描移除的過期資料列數。|  
|**接觸到的虛設過期資料列/秒**|(平均) 每秒虛設掃描接觸到的過期資料列數。|  
|**接觸到的虛設將過期資料列/秒**|(平均) 每秒虛設掃描接觸到的將過期資料列數。|  
|**接觸到的虛設項目列/秒**|(平均) 每秒虛設掃描接觸到的資料列數。|  
|**啟動的虛設掃描/秒**|(平均) 每秒啟動的虛設掃描次數。|  
  
## <a name="see-also"></a>另請參閱  
 [XTP &#40;記憶體內部 OLTP&#41; 效能計數器](../../integration-services/performance/performance-counters.md)  
  
  
