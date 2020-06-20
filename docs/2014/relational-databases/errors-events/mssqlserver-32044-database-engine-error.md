---
title: MSSQLSERVER_32044 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32044 (Database Engine error)
ms.assetid: f2d073be-d9a1-4837-8a38-028d3e3403bd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d41e9cb873c2152aaab26e5c8f789391670b4305
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033911"
---
# <a name="mssqlserver_32044"></a>MSSQLSERVER_32044
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|32044|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum32044|  
|訊息文字|已發出 [鏡像認可負擔] 的警示。 目前的值 '%d' 已超出臨界值 '%d'。|  
  
## <a name="explanation"></a>說明  
 這個資料庫鏡像事件是在主體伺服器執行個體上發出，用來指示由於資料庫鏡像，彙總認可等待時間已達到或超出使用者指定的臨界值。 等待時間是交易數目和各交易時間的乘積。 例如，下列情況都會產生 1000 毫秒等待時間：1000 筆交易 * 1 毫秒，以及 1 筆交易 \* 1000 毫秒。 交易計數激增、傳送記錄延遲，或是排清鏡像伺服器執行個體上的記錄延遲，都可能會使認可等待時間增加。  
  
 鏡像認可負擔量是一項效能標準，可協助您評估目前同步作業的效能衝擊。 這項標準只有在高安全性模式中才會相關。 由於高安全性模式是同步的，主體伺服器執行個體會在傳送記錄給鏡像伺服器執行個體之後，等待認可交易，直到接到鏡像伺服器執行個體已將記錄寫入磁碟的確認為止。 在等待還原至鏡像資料庫的同時，記錄會一直保留在鏡像伺服器執行個體的磁碟上。  
  
## <a name="user-action"></a>使用者動作  
 檢查主體和鏡像伺服器執行個體上的負載及其網路連接，以了解發生原因。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [使用鏡像效能標準的警告臨界值與警示 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
