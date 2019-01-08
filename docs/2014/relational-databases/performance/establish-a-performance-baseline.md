---
title: 建立效能基準 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], baselines
- monitoring performance [SQL Server], baselines
- tuning databases [SQL Server], baselines
- server performance [SQL Server], baselines
- performance [SQL Server], baselines
- baseline performance [SQL Server]
- measurements for baseline statistics [SQL Server]
- monitoring server performance [SQL Server], establishing baseline
- database monitoring [SQL Server], baselines
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4b382545e9f7e5af1607d67539f2ae9f29cfdce3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774550"
---
# <a name="establish-a-performance-baseline"></a>建立效能基準
  若要判斷您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統是否以最佳方式執行，請長時間定期測量效能 (即使沒有問題發生)，以建立伺服器效能基準。 請將每個新的組測量的結果與先前的測量進行比較。  
  
 以下各方面會影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的效能：  
  
-   系統資源 (硬體)  
  
-   網路架構  
  
-   作業系統  
  
-   資料庫應用程式  
  
-   用戶端應用程式  
  
 至少需使用基準線測量來判斷：  
  
-   作業的尖峰與離峰期間。  
  
-   產生查詢或批次命令的回應時間。  
  
-   資料庫備份與還原的完成時間。  
  
 建立伺服器效能基準線之後，請將基準線統計資料表與目前的伺服器效能進行比較。 與基準線差距過高或過低的數值即為必須進一步調查的候選項目。 這些項目可能代表必須調整或重設設定的範圍。 例如，當執行一組查詢的時間量增加時，請檢查查詢以判斷是否可以重寫查詢，或者是否必須加入資料行統計資料或新的索引。  
  
## <a name="see-also"></a>另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
