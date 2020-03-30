---
title: 加速資料庫復原 | Microsoft Docs
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- accelerated database recovery [SQL Server], recovery-only
- database recovery [SQL Server]
author: mashamsft
ms.author: mathoma
ms.reviewer: kfarlee
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 58c31d9b5e0e8858cc1953a2961107caea08d381
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "80342520"
---
# <a name="accelerated-database-recovery"></a>加速資料庫復原

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

加速資料庫復原 (ADR) 藉由重新設計 SQL 的資料庫引擎復原處理序來提升資料庫可用性，尤其是針對長時間執行的交易。 ADR 是 SQL Server 2019 的新功能，也適用於 Azure SQL Database 中的單一資料庫和集區資料庫，以及 Azure SQL 資料倉儲中的資料庫 (目前處於公開預覽狀態)。 ADR 的主要優點為：

- **快速且一致的資料庫復原**

  使用 ADR，長時間執行的交易便不會影響整體復原時間，可快速且一致地進行資料庫復原，不論系統內使用中的交易數或其大小為何。

- **瞬間交易回復**

  使用 ADR，交易回復會在瞬間完成，不論交易處於使用中狀態的時間長度，或是已執行的更新數為何。

- **積極性記錄截斷**

  使用 ADR，交易記錄會積極地進行截斷，即使有使用中的長時間執行交易，它也能防止其失去控制。

## <a name="the-current-database-recovery-process"></a>目前的資料庫復原處理序

若沒有 ADR，SQL Server 中的資料庫復原會遵循 [ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf) 復原模型且由三個階段組成，如下圖所示，並會在圖表之後會有更詳細的說明。

![目前的復原處理序](./media/accelerated-database-recovery-concepts/current-recovery-process.png)

- **分析階段**

  SQL Server 會從最後一次成功檢查點 (或是最舊的中途分頁 LSN) 的開頭順向掃描交易記錄至結尾，以判斷 SQL Server 停止時每個交易的狀態。

- **重做階段**

  SQL Server 會從最舊的未認可交易開始，執行交易記錄的順向掃描到結尾，藉由重做所有已認可的作業，讓資料庫回到當機時的狀態。

- **復原階段**

  針對當機時每一個使用中的交易，SQL Server 會向後周遊記錄，復原此交易所執行的作業。

根據這項設計，資料庫引擎從未預期重新啟動進行復原所需時間 (大約) 會和當機時系統中使用時間最長交易的大小成比例。 復原需要回復所有未完成的交易。 所需時間與交易執行的工作和其已使用時間成比例。 因此，SQL Server 復原處理序在有長時間執行的交易 (例如大量插入作業或針對大型資料表的索引建置作業) 時，可能需要相當長的時間。

此外，根據此設計，取消或復原大型交易也可能會耗費相當長的時間，因為它會使用與上述相同的復原復原階段。

此外，資料庫引擎在有長時間執行交易時無法截斷交易記錄，因為復原和回復處理序需要它們對應的記錄檔記錄。 因此，有些交易記錄會變得相當龐大並耗用大量的磁碟機空間。

## <a name="the-accelerated-database-recovery-process"></a>加速資料庫復原處理序

ADR 藉由完全重新設計資料庫引擎的復原處理序來解決上述問題：

- 透過避免從最舊使用中交易的開頭進行掃描，或是掃描至開頭，來固定時間或使其能夠立即完成。 使用 ADR，只會從最後一次成功的檢查點 (或是最舊的中途分頁記錄序號 (LSN)) 開始處理交易記錄。 因此，復原時間不會受到長時間執行的交易影響。
- 將所需的交易記錄空間減至最小，因為不再需要處理整個交易的記錄。 因此，可在進行檢查點和備份時積極地截斷交易記錄。

從高層級而言，ADR 會透過對所有實體資料庫修改建立版本，並只復原邏輯作業 (其數量有限且可以立即進行復原) 來快速地進行資料庫復原。 任何在當機時處於使用中狀態的交易都會標記為中止，且因此並行使用者查詢可以略過任何由這些交易產生的版本。

ADR 復原處理序與目前復原處理序具有相同的三個階段。 這些階段與 ADR 運作的方式如下圖所示。

![ADR 復原處理序](./media/accelerated-database-recovery-concepts/adr-recovery-process.png)

- **分析階段**

  處理序與目前的處理序相同，但會加上重新建構 sLog 並複製未建立版本作業的記錄檔記錄。
  
- **重做**階段

  分成兩個子階段
  - 子階段 1

      從 sLog 重做 (最舊的未認可交易至最後一個檢查點)。 重做是快速的作業，因為它只需要處理來自 sLog 的幾個記錄。

  - 子階段 2

     從最後一個檢查點開始 (而非最舊的未認可交易)，從交易記錄進行重做
     
- **復原階段**

   ADR 的復原階段會搭配邏輯還原來使用 sLog 以復原未建立版本的作業及持續版本存放區 (PVS)，以幾乎立即的方式來完成執行資料列版本式復原。

您也可以觀看這段說明加速資料庫復原的 8 分鐘影片

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Advanced-Database-Recovery--Data-Exposed/player?WT.mc_id=dataexposed-c9-niner]

## <a name="adr-recovery-components"></a>ADR 復原元件

ADR 的四個關鍵元件為：

- **持續版本存放區 (PVS)**

  持續版本存放區是一種資料庫引擎機制，用於保存資料庫本身產生的資料列版本，而非傳統的 `tempdb` 版本存放區。 PVS 可隔離資源並改善可讀取次要的可用性。

- **邏輯還原**

  邏輯還原是非同步的處理序，負責執行資料列層級版本式復原，為所有建立版本的作業提供交易立即回復和復原。

  - 追蹤所有中止的交易
  - 針對所有使用者交易，使用 PVS 來執行復原
  - 在交易中止後立即釋出所有鎖定

- **sLog**

  sLog 是一種次要的記憶體內部記錄串流，其儲存未建立版本作業的記錄檔記錄 (例如中繼資料快取無效判定、取得鎖定等)。 sLog 是：

  - 體積小並位於記憶體內部
  - 透過在檢查點處理序期間進行序列化來保存在磁碟上
  - 在交易認可時定期截斷
  - 透過只處理未建立版本的作業來加速重做和復原  
  - 透過只保留需要的記錄檔記錄來啟用積極性交易記錄截斷

- **清除工具**

  清除工具是一種非同步處理序，會定期喚醒並清理不需要的分頁版本。

## <a name="who-should-consider-accelerated-database-recovery"></a>應考慮加速資料庫復原的對象

建議下列類型的客戶考慮啟用 ADR：

- 具有長時間執行交易工作負載的客戶。
- 曾經歷使用中交易造成交易記錄大幅成長的客戶。  
- 曾經歷因 SQL Server 長時間執行的復原 (例如未預期的 SQL Server 重新啟動或手動交易回復) 而導致資料庫長期無法提供使用的客戶。


## <a name="see-also"></a>另請參閱  

  
