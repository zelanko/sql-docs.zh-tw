---
title: 索引作業的交易記錄磁碟空間 | Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index disk space [SQL Server]
- space [SQL Server], indexes
- transaction logs [SQL Server], disk space
- disk space [SQL Server], transaction logs
- space [SQL Server], transaction logs
ms.assetid: 4f8a4922-4507-4072-be67-c690528d5c3b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8a88bbccbe0fd1a57455343858f463afe072ed99
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722319"
---
# <a name="transaction-log-disk-space-for-index-operations"></a>索引作業的交易記錄磁碟空間
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  大規模的索引作業會產生大量資料載入，而造成交易記錄檔迅速填滿。 為了確保索引作業可以回復，在索引作業完成之前，交易記錄檔不得遭到截斷；不過，在索引作業期間可以備份記錄檔。 因此，交易記錄檔必須有足夠空間來儲存索引作業交易，以及索引作業期間的任何並行使用者交易。 不管是離線或線上索引作業都是如此。 因為在離線索引作業期間無法存取基礎資料表，所以使用者交易不多，記錄檔應該不會成長太快。 線上索引作業並不禁止並行使用者活動，因此大規模的線上索引作業若再結合大量的並行使用者交易，會造成交易記錄檔持續成長，同時又無法截斷記錄檔。  
  
## <a name="recommendations"></a>建議  
 當您執行大規模的索引作業時，請考慮下列建議：  
  
1.  確定在執行線上大規模索引作業之前已備份及截斷交易記錄檔，且記錄檔有足夠空間可儲存預計的索引和使用者交易。  
  
2.  針對索引作業，請考慮將 SORT_IN_TEMPDB 選項設為 ON。 這樣可將索引交易與並行使用者交易區分開來。 索引交易將儲存在 **tempdb** 交易記錄檔中，並行使用者交易則儲存在使用者資料庫的交易記錄檔中。 這樣可在索引作業期間，讓使用者資料庫的交易記錄檔進行截斷 (如果有此需要的話)。 另外，如果 **tempdb** 記錄檔與使用者資料庫記錄檔不在同一個磁碟上，這兩個記錄檔就不會競爭相同的磁碟空間。  
  
    > [!NOTE]  
    >  確認 **tempdb** 資料庫和交易記錄檔有足夠的磁碟空間可處理索引作業。 要等到索引作業完成之後，才能截斷 **tempdb** 交易記錄檔。  
  
3.  使用資料庫復原模式，可使索引作業的記錄量減至最少。 這樣會減少記錄檔大小，防止記錄填滿記錄檔空間。  
  
4.  不要在外顯交易中執行線上索引作業。 這樣需等到外顯交易結束之後，才能截斷記錄檔。  
  
## <a name="related-content"></a>相關內容  
 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [索引磁碟空間範例](../../relational-databases/indexes/index-disk-space-example.md)  
  
  
