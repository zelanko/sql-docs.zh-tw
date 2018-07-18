---
title: MSSQLSERVER_17884 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c7c281794f5926b641361165b4b6614129afdbe0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409907"
---
# <a name="mssqlserver17884"></a>MSSQLSERVER_17884
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|17884|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SRV_SCHEDULER_DEADLOCK|  
|訊息文字|在過去的 %d 秒內，工作者執行緒未在節點 %d 上收取到指派給處理序的新查詢。 這種狀況可能是由封鎖或長時間執行的查詢所造成，且可能會對用戶端的回應時間造成負面影響。 請使用 "max worker threads" 組態選項以增加允許的執行緒數目，或最佳化目前執行中的查詢。  SQL 處理序使用率: %d%%。 系統閒置率: %d%%。|  
  
## <a name="explanation"></a>說明  
 每個排程器都沒有進度的徵兆，而且可能是由於死結所造成，因為沒有任何執行緒可以進行及/或沒有新的工作可挑選和處理。 如果處理序使用率很低，則電腦上的其他處理序可能會導致伺服器處理序 CPU 資源用盡。  
  
## <a name="user-action"></a>使用者動作  
 判斷為何產生封鎖而且沒有任何進度，並據以解決此狀況。 如果處理序使用率很低，請檢查其他處理序所造成的系統負載。  
  
  
