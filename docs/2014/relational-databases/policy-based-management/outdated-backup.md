---
title: 過期的備份 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 307a4ad0-675a-4f97-9a3c-cedd61bdfae5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bcdfc02c06117529c2f09621197728f3c9e77dc1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253156"
---
# <a name="outdated-backup"></a>過期的備份
  這個規則會檢查資料庫是否有最新備份。 排程定期備份對於保護資料庫避免因為許多不同失敗而造成資料遺失而言，是很重要的工作。 備份資料的適當頻率取決於資料庫的復原模式、有關可能資料遺失的商業需求及資料庫的更新頻率。 在經常更新的資料庫中，備份之間的工作損失風險會快速地增加。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 我們建議您要更常執行備份，以防止資料庫遭受資料遺失。  
  
 簡單復原模式和完整復原模式都需要資料備份。 在這兩種復原模式中，您都可以使用差異備份來補充完整備份，如此可有效率地減少資料遺失的風險。  
  
 如果是使用完整復原模式的資料庫，我們建議您進行經常性的記錄備份。 如果是包含非常重要之資料的實際執行資料庫，通常會每隔 1 到 15 分鐘進行一次記錄備份。  
  
> [!NOTE]  
>  建議的排程備份方法是資料庫維護計畫。  
  
## <a name="for-more-information"></a>詳細資訊  
 [系統資料庫的備份與還原 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [復原模式 &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)  
  
 [建立差異資料庫備份 &#40;SQL Server&#41;](../backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 [建立完整資料庫備份 &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)  
  
 [維護計畫](../maintenance-plans/maintenance-plans.md)  
  
 [交易記錄備份 &#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
