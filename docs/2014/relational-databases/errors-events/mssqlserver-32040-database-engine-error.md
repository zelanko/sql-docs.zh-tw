---
title: MSSQLSERVER_32040 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32040 (Database Engine error)
ms.assetid: 709219b1-f8b2-4696-8923-dd2e91492eb8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 198a58816388a1f5c80b45b776548508f01a1c73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914267"
---
# <a name="mssqlserver32040"></a>MSSQLSERVER_32040
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|32040|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum32040|  
|訊息文字|已發出 [最舊尚未傳送的交易] 的警示。 目前的值 '%d' 已超出臨界值 '%d'。|  
  
## <a name="explanation"></a>說明  
 這個資料庫鏡像事件是在主體伺服器執行個體上發出，用來指示最久未傳送交易的時間已經到達使用者指定的臨界值。 一般而言，會發生這個事件，是因為系統效能已經變更。 若不是兩個系統間的頻寬已經縮減，就是負載已經增加。  
  
 最久未傳送交易的時間是以未傳送交易的分鐘數計算，可協助您評估資料遺失可能性的效能標準。 這項標準與高效能模式的工作階段尤其相關。 但是，當鏡像因為夥伴中斷連接而暫停或暫止時，這項標準也會與高安全性模式工作階段有關。  
  
## <a name="user-action"></a>使用者動作  
 檢查主體和鏡像伺服器執行個體上的負載及其網路連接，以了解發生原因。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [使用鏡像效能標準的警告臨界值與警示 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
