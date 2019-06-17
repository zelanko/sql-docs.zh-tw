---
title: 正在載入伺服器容量計劃-Analytics Platform System |Microsoft Docs
description: 這個容量規劃工作表可協助您判斷針對載入到 Analytics Platform System Parallel Data Warehouse 的資料載入伺服器的需求。 」
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2f0efd7e0688496d5af7887431ca00ae683c874f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213410"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>Analytics Platform System 載入伺服器容量規劃工作表
這個容量規劃工作表可協助您判斷將資料載入至 SQL Server PDW 的載入伺服器的需求。 使用此選項來建立您的計劃購買或佈建現有的載入伺服器。  
  
## <a name="worksheet-notes"></a>工作表的附註
  
1.  此工作表適用於正在載入資料的伺服器**dwloader**命令列載入工具。  
  
2.  如需載入 Integration Services 或協力廠商載入工具與資料，需求可以而有所不同，載入程序的差異。  
  
3.  大部分需求套用至載入其中一個壓縮或未壓縮資料檔案在 [需求] 的任何差異會註明，以粗體顯示。  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![剪貼簿](media/clipboard-icon.png "剪貼簿")容量規劃工作表  
  
列印這張工作表，並填入您自己的需求。  
  
|元件|需求|在您自己的需求與此欄位填入|建議|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|儲存體|您計劃來載入伺服器上儲存在任何給定的一段時間的最大位元組。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要判斷儲存體需求，找出您打算在任何給定的一段時間中載入伺服器上儲存的資料量。  容量需求適用於僅載入檔案作業系統和載入檔案應該位於不同的磁碟陣列上。<br /><br />例如：如果您打算從磁碟 3 次載入 100 GB 資料的每一天，但不是刪除資料檔案，直到最後一週，則您需要最小的 2.1 TB，來儲存資料檔案。 我們建議您正在執行作保守估計，取得關於 30%以上的儲存體帳戶差異和成長。  此範例中，2.73 TB 的儲存空間會是更好。|  
|載入速率|每小時的資料載入 PDW 的最大位元組。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|這是估計值。 在計算此需求，假設檔案已載入在伺服器上，和其他載入條件所說的可能。<br /><br />例如：不需要納入資料可壓縮性，須，因為 dwloader 一律會傳送未壓縮資料與 PDW。 不是需要納入資料類型轉換和目的地資料表的大小。|  
|Network|網路連線類型。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|判斷負載速率需求的最佳網路連線類型。<br /><br />例如：InfiniBand 或 10 Gbit 乙太網路會提供最佳的載入速度。 1 Gbit 乙太網路會限制負載比率為 360 GB 每小時或更少。|  
|I/O|每小時的讀取和寫入的位元組。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要載入資料，dwloader 必須讀取的所有資料從磁碟再將它傳送至 PDW。<br /><br />每個載入伺服器無法設備可以接收所有載入來源的資料快速載入資料。 若要節省成本，規劃的 I/O 讀取載入，讓它不會超過設備的負載容量的容量。<br /><br />例如：<br />PDW 接收，並將資料載入至最大速率 1.8 TB 的每小時 1 機架應用裝置。 有 2 個或多個機架應用裝置，最大負載比率會是每小時 3.6 TB。<br /><br />如果您打算同時載入多個載入伺服器，每個載入伺服器的 I/O 需求會少於一部伺服器執行所有的載入。<br /><br />例如：載入伺服器可以載入 1.8 TB 的最多每小時 1 機架應用裝置。 兩個載入伺服器可能每個同時載入 900 GB 每小時 1 機架應用裝置。 更高層級的並行處理可以降低效率和最大輸送量。<br /><br />I/O 容量考量帳戶所有載入伺服器上發生的 I/O。 如果載入伺服器有其他的 I/O 資料流，除了資料載入，例如從 ETL 伺服器，接收資料檔會增加的 I/O 需求。<br /><br />壓縮的資料，I/O 需求取決於資料壓縮率。 dwloader 讀取壓縮的資料，然後將它解壓縮再將它傳送至 PDW。 較高的壓縮率，較少的資料載入伺服器必須從磁碟讀取。<br /><br />例如：如果必要的負載速率是 1.8 TB 每小時，且資料會儲存在 2:1 壓縮載入伺服器，然後載入伺服器只需要每小時而不是 1.8 TB 的磁碟讀取 900 GB。 3:1 壓縮比率表示載入伺服器需要每小時從磁碟讀取有 600 GB。|  
|CPU|插槽的數目。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|如需載入未壓縮的資料，dwloader 不是需要大量 CPU 的應用程式。  最小的需求，我們建議使用最近製造 2 通訊端伺服器。<br /><br />如需載入壓縮的資料，您需要足夠的 CPU 能力，來解壓縮資料，再將它傳送至 PDW。 dwloader 可以同時執行 10 個作用中的執行緒。 如果您打算同時載入 10 個壓縮的檔案，我們建議的伺服器具有最少 10 核心 CPU 或兩個 6 核心 Cpu。|  
|RAM|GB 的記憶體中快取檔案期間，Windows 會載入。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|dwloader 載入伺服器上，使用極少的 RAM。 為了效能，Windows 會使用快取載入檔案之後從磁碟讀取的記憶體。<br /><br />若要判斷的 RAM 需求，請參閱 Windows Server 安裝和任何第 3 個合作對象應用程式的需求。 如果您沒有從其他來源的需求，我們建議至少 32 GB。<br /><br />壓縮的資料，更快速的 RAM 很有用，因為它將會加速解壓縮。|  
  
## <a name="see-also"></a>另請參閱  
[取得並設定載入伺服器](acquire-and-configure-loading-server.md)  
[dwloader 命令列載入器](dwloader.md)  
  
