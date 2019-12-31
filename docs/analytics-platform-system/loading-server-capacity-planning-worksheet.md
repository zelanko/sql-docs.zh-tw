---
title: 正在載入伺服器容量規劃
description: 此容量規劃工作表可協助您判斷載入伺服器將資料載入至分析平臺系統平行處理資料倉儲的需求。」
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 7dded8c79495d0bdc684927f4875a93c3160c1bf
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401036"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>正在載入分析平臺系統的伺服器容量規劃工作表
此容量規劃工作表可協助您判斷載入伺服器將資料載入 SQL Server PDW 的需求。 使用此功能來建立您的方案，以購買或布建現有的載入伺服器。  
  
## <a name="worksheet-notes"></a>工作表附注
  
1.  此工作表適用于將使用**dwloader**命令列載入工具載入資料的伺服器。  
  
2.  若要使用 Integration Services 或協力廠商載入工具來載入資料，需求會根據載入程式的差異而有所不同。  
  
3.  大部分的需求都適用于載入壓縮或未壓縮的資料檔案;需求的任何差異都以粗體顯示。  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![剪貼](media/clipboard-icon.png "剪貼簿")簿容量規劃工作表  
  
列印此工作表，並以您自己的需求填入。  
  
|元件|需求|請在此資料行中填入您自己的需求|建議|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|儲存體|您計畫在任何指定的時間儲存在載入伺服器上的最大位元組數。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要判斷儲存需求，請找出您計畫在任何指定時間儲存在載入伺服器上的資料量。  容量需求僅適用于載入檔案;作業系統和載入檔案應該位於不同的磁片陣列上。<br /><br />例如：如果您打算每天從磁片載入 100 GB 的資料，但在一周結束前不會刪除資料檔案，則您需要至少 2.1 TB 來儲存資料檔案。 我們建議您保守，並取得大約30% 的儲存體，以考慮差異和成長。  在此範例中，2.73 TB 的儲存空間會較佳。|  
|載入速率|要載入 PDW 的資料每小時最大位元組數。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|這是估計值。 在計算這項需求時，假設檔案已經在載入伺服器上，而且其他載入條件越好。<br /><br />例如：不需要在資料 compressibility 中納入考慮，因為 dwloader 一律會將未壓縮的資料傳送至 PDW。 不需要考慮資料類型轉換和目的地資料表的大小。|  
|網路|網路連線類型。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|判斷您的負載速率需求的最佳網路連線類型。<br /><br />例如：不充分或 10 Gb 的 Ethernet 會提供最佳的載入速度。 1 gb Ethernet 會將負載速率限制為每小時 360 GB 或更少。|  
|I/O|讀取和寫入的每小時位元組數。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要載入資料，dwloader 必須先從磁片讀取所有資料，然後再將它傳送至 PDW。<br /><br />每個載入伺服器的載入資料速度，都無法比設備接收來自所有載入來源的資料更快。 若要節省成本，請規劃用於載入的 i/o 讀取容量，使其不會超過設備的負載容量。<br /><br />例如：<br />PDW 會以每小時 1.8 TB 的最高速率，接收並將資料載入1個機架的設備。 針對具有2個或更多機架的設備，最大負載速率為每小時 3.6 TB。<br /><br />如果您打算同時從多部載入伺服器載入，每個載入伺服器的 i/o 需求將會小於一台伺服器執行所有載入的時間。<br /><br />例如：一部載入伺服器每小時最多可以載入1個機架設備的 1.8 TB。 兩部載入伺服器每小時可以並行900載入1個機架的應用裝置。 較高的並行層級可以降低效率和最大輸送量。<br /><br />針對 i/o 容量，請考慮載入伺服器上發生的所有 i/o。 如果載入伺服器除了資料載入之外還有其他 i/o 流量（例如從 ETL 伺服器接收資料檔案），i/o 需求也會增加。<br /><br />針對壓縮的資料，i/o 需求取決於資料壓縮速率。 dwloader 會讀取壓縮的資料，然後在將它傳送至 PDW 之前加以 uncompresses。 壓縮比率越高，載入伺服器需要從磁片讀取的資料就越少。<br /><br />例如：如果所需的負載速率是每小時 1.8 TB，而且資料儲存在具有2:1 壓縮的載入伺服器上，則載入伺服器只需要從磁片讀取每小時 900 GB，而不是 1.8 TB。 3:1 壓縮比率表示載入伺服器需要從磁片讀取每小時 600 GB。|  
|CPU|通訊端數目。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要載入未壓縮的資料，dwloader 不是需要大量 CPU 的應用程式。  為最低需求，建議使用最近製造的2通訊端伺服器。<br /><br />若要載入壓縮的資料，您需要有足夠的 CPU 功能來解壓縮資料，然後再將它傳送至 PDW。 dwloader 可以一次執行10個使用中線程。 如果您打算同時載入10個壓縮檔案，建議伺服器至少具有10核心 CPU 或兩個6核心 cpu。|  
|RAM|在載入期間允許 Windows 快取檔案的記憶體 GB。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|dwloader 在載入伺服器上使用極少的 RAM。 為了提高效能，Windows 會在從磁片讀取檔案之後，使用記憶體來快取載入的檔案。<br /><br />若要判斷 RAM 需求，請參閱您的 Windows Server 安裝和任何協力廠商應用程式需求。 如果您沒有其他來源的需求，建議您至少使用 32 GB。<br /><br />針對壓縮的資料，更快的 RAM 會很有用，因為它會加速解壓縮。|  
  
## <a name="see-also"></a>另請參閱  
[取得並設定載入伺服器](acquire-and-configure-loading-server.md)  
[dwloader 命令列載入器](dwloader.md)  
  
