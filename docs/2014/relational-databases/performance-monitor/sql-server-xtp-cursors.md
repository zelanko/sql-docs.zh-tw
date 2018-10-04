---
title: XTP 資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d31540020df2a4aa4f30f144de4d7e606b471e9e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096998"
---
# <a name="xtp-cursors"></a>XTP 資料指標
  XTP 資料指標效能物件包含與內部 XTP 引擎資料指標相關的計數器。 低層級的建置組塊 XTP 引擎用來處理資料指標是[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢。 因此，您通常不會有這些指標的直接控制權。  
  
 下表描述**XTP 資料指標**計數器。  
  
|計數器|描述|  
|-------------|-----------------|  
|**資料指標刪除/秒**|(平均) 每秒資料指標刪除數目。|  
|**資料指標插入/秒**|(平均) 每秒資料指標插入數目。|  
|**啟動的資料指標掃描/秒**|(平均) 每秒啟動的資料指標掃描次數。|  
|**資料指標唯一違規/秒**|(平均) 每秒唯一約束違規數目。|  
|**資料指標更新/秒**|(平均) 每秒資料指標更新數目。|  
|**資料指標寫入衝突/秒**|(平均) 每秒寫至相同資料列版本的寫入 - 寫入衝突數目。|  
|**塵封角落掃描重試次數/秒 (由使用者發出)**|使用者完整資料表掃描發出的塵封角落掃掠期間，(平均) 每秒因為發生寫入衝突而進行掃描的重試次數。 這是層級非常低的計數器，非供客戶使用。|  
|**移除的過期資料列/秒**|(平均) 每秒由資料指標移除的過期資料列數。|  
|**接觸到的過期資料列/秒**|(平均) 每秒資料指標接觸到的過期資料列數。|  
|**傳回的資料列/秒**|(平均) 每秒由資料指標傳回的資料列數。|  
|**接觸到的資料列/秒**|(平均) 每秒資料指標接觸到的資料列數。|  
|**接觸到的暫訂刪除資料列/秒**|(平均) 每秒資料指標接觸到的將過期資料列數。 如果刪除資料列的交易仍為使用中 (也就是尚未認可或中止)，則資料列即將過期。|  
  
## <a name="see-also"></a>另請參閱  
 [XTP&#40;記憶體內部 OLTP&#41;效能計數器](../../integration-services/performance/performance-counters.md)  
  
  
