---
title: 使用查詢存放區的工作負載調整資料庫 | Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Engine Tuning Advisor, Query Store
ms.assetid: 17107549-5073-4fa2-8ee7-5ed33b38821e
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f86c3add785f38ea483199333478cea2d1d5634e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="tuning-database-using-workload-from-query-store"></a>使用查詢存放區的工作負載調整資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


SQL Server 中的[查詢存放區](../../relational-databases/performance/how-query-store-collects-data.md)功能可自動擷取查詢、計畫和執行階段統計資料的記錄，並將這項資訊保存在資料庫中。 [Database Engine Tuning Advisor (DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md) 支援新選項，可使用查詢存放區自動選取適當的工作負載以進行調整。 對於許多使用者而言，這可消除明確收集工作負載進行調整的需要。 只有已開啟「查詢存放區」功能的資料庫才能使用這項功能。 
  
  SQL Server Management Studio **16.4** 版或更高版本中提供了此功能。 
  
<a name="how-to-tune-a-workload-from-query-store-in-database-engine-tuning-advisor-gui"></a>如何在 Database Engine Tuning Advisor GUI 中調整查詢存放區的工作負載
---
從 DTA GUI 中，選取 [一般]窗格中的 [查詢存放區] 選項按鈕，即可啟用此功能 (請參閱下圖)。
![查詢存放區的 DTA 工作負載](../../relational-databases/performance/media/dta-workload-from-query-store.gif)
 
<a name="how-to-tune-a-workload-from-query-store-in-dtaexe-command-line-utility"></a>如何在 dta.exe 命令列公用程式中調整查詢存放區的工作負載
---
從命令列 (dta.exe) 中，選擇 **-iq** 選項，以選取查詢存放區的工作負載。 

有另外兩個選項可透過命令列，協助您從查詢存放區中選取工作負載時，調整 DTA 的行為。 透過 GUI 無法使用這些選項：
  1. 要調整的工作負載事件數目︰使用 **-n** 命令列引數指定的這個選項，可讓使用者控制查詢存放區中調整的事件數目。 根據預設，DTA 會針對此選項使用 1000 這個值。 請注意，DTA 一律會選擇總持續期間最耗費資源的事件數。 
  
  2. 要調整的事件時間範圍︰ 因為查詢存放區可能包含很久以前執行的查詢，此選項可讓使用者指定過去的時間範圍 (以時數為單位)，只有在此時間範圍執行的查詢，DTA 才會考慮進行調整。 您可以使用 **-I** 命令列引數來指定此選項。 

如需詳細資訊，請參閱 [dta 公用程式](../../tools/dta/dta-utility.md)。

<a name="difference-between-using-workload-from-query-store-and-plan-cache"></a>使用查詢存放區與計畫快取的工作負載之間的差異 
--- 
查詢存放區和計畫快取選項之間的差異在於，前者包含已針對資料庫執行之查詢的長期記錄，這些查詢會在伺服器重新啟動時持續保存。 而另一方面，計畫快取只包含最近執行之查詢 (其計畫快取到記憶體中) 的子集。 當伺服器重新啟動時，就會捨棄計畫快取中的項目。

<a name="see-also"></a>另請參閱 
--- 
[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)     
[教學課程：Database Engine Tuning Advisor](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)     
[查詢存放區如何收集資料](../../relational-databases/performance/how-query-store-collects-data.md)     
[查詢存放區的最佳做法](../../relational-databases/performance/best-practice-with-the-query-store.md)
