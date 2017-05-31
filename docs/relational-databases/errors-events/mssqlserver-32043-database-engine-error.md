---
title: MSSQLSERVER_32043 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4f4a6d7b4331e1e7953b80d825a638321808ef82
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver32043"></a>MSSQLSERVER_32043
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|32043|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum32043|  
|訊息文字|已發出 [未還原的記錄] 的警示。 目前的值 '%d' 已超出臨界值 '%d'。|  
  
## <a name="explanation"></a>說明  
這個資料庫鏡像事件是在鏡像伺服器執行個體上發出，用來指示未還原記錄數量已經到達使用者指定的臨界值。 一般而言，會發生這個事件，是因為系統效能已經變更。 若不是兩個系統間的頻寬已經縮減，就是負載已經增加。  
  
未還原的記錄是指，已由鏡像伺服器執行個體接收且寫入磁碟，但正等待還原至鏡像資料庫的記錄。 未還原記錄的數量是以 KB 為單位，可協助您評估目前容錯移轉時間的效能標準。 容錯移轉所花費最主要的時間是套用未還原的記錄，還有一些零星時間則是用來復原資料庫並讓它上線。  
  
> [!NOTE]  
> 如果是自動容錯移轉，則系統發現錯誤的時間與容錯移轉時間無關。  
  
## <a name="user-action"></a>使用者動作  
檢查主體和鏡像伺服器執行個體上的負載及其網路連接，以了解發生原因。  
  
## <a name="see-also"></a>另請參閱  
[資料庫鏡像 &#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[使用鏡像效能標準的警告閾值與警示 &#40;SQL Server&#41;](~/database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  

