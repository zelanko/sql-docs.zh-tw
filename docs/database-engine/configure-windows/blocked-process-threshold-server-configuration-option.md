---
title: 已封鎖的處理序臨界值伺服器組態選項 | Microsoft Docs
description: 了解如何使用已封鎖處理序臨界值選項來指定 SQL Server 產生已封鎖處理序報表及發出警示的間隔。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- thresholds [SQL Server]
- blocked process threshold option
ms.assetid: 3d46d143-bc6a-4220-8b55-6baa37547c25
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bdd5f7d01e7271609562fb7d42126746d6163de4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725239"
---
# <a name="blocked-process-threshold-server-configuration-option"></a>已封鎖的處理序臨界值伺服器組態選項
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

 使用 **blocked process threshold** 選項，以秒為單位來指定產生已封鎖處理序報表的臨界值。 此臨界值可設定為 5 到 86,400 之間的值。  鎖定監視器只會每隔 5 秒喚醒一次以偵測封鎖條件 (其會尋找其他條件，例如鎖死)。 因此，如果將「已封鎖的處理序臨界值」設為 1，則其將不會偵測到已封鎖 1 秒的處理序。 其可偵測已封鎖處理序的最短時間為 5 秒。
 
 預設不會針對已封鎖的處理序產生任何報告。 對於系統工作或在等待不產生可偵測死結的資源的工作，並不會產生此事件。  
  
 您可以定義在產生此事件時要執行的 [警示](../../ssms/agent/alerts.md) 。 例如，您可以選擇呼叫管理員，以採取適當的動作來處理此封鎖狀況。  
  
 封鎖的處理序臨界值使用死結監視背景執行緒，瀏覽等待時間超過設定的臨界值或是臨界值的好幾倍之工作清單。 每隔一段報告時間間隔就會為每個已封鎖的工作產生一次此事件。  
  
 封鎖的處理序報表是以最大速率來執行。 不保證即時或甚至接近即時的報告。  
  
 設定立即生效，伺服器不必停止再重新啟動。  
  
## <a name="examples"></a>範例  
 下例範例將 `blocked process threshold` 設為 `20` 秒，為每一個封鎖的工作產生封鎖處理序報表。  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 20 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Blocked Process Report 事件類別](../../relational-databases/event-classes/blocked-process-report-event-class.md)  
  
  
