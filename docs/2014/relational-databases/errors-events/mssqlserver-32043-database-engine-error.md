---
title: MSSQLSERVER_32043 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1db8560c2197ef95f01e7dd66a711d4b7a225646
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053952"
---
# <a name="mssqlserver_32043"></a>MSSQLSERVER_32043
    
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
>  如果是自動容錯移轉，則系統發現錯誤的時間與容錯移轉時間無關。  
  
## <a name="user-action"></a>使用者動作  
 檢查主體和鏡像伺服器執行個體上的負載及其網路連接，以了解發生原因。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [使用鏡像效能標準的警告臨界值與警示 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
