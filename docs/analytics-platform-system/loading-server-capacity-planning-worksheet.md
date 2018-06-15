---
title: 載入伺服器容量計劃-Analytics Platform System |Microsoft 文件
description: 這個容量規劃工作表可協助您判斷載入 Analytics Platform System 平行資料倉儲的資料載入伺服器的需求。 」
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2f0efd7e0688496d5af7887431ca00ae683c874f
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539438"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>載入分析平台系統伺服器容量規劃工作表
這個容量規劃工作表可協助您判斷資料載入 SQL Server PDW 載入伺服器的需求。 使用此選項來建立您的計劃購買或佈建現有載入伺服器。  
  
## <a name="worksheet-notes"></a>工作表的資訊
  
1.  此工作表適用於正在載入具有資料的伺服器**dwloader**命令列載入工具。  
  
2.  載入 Integration Services 或協力廠商合作對象載入工具與資料，可以視需求有所不同載入程序的差異。  
  
3.  大部分的需求會套用至載入壓縮或未壓縮資料檔案。以粗體顯示註明需求的任何差異。  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![剪貼簿](media/clipboard-icon.png "剪貼簿")容量規劃工作表  
  
列印此工作表，並填入您自己的需求。  
  
|元件|需求|在您自己的需求與此資料行填滿|建議|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|儲存空間|您計劃在任何給定的一段時間來載入伺服器上儲存的位元組上限。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要判斷儲存體需求，找出您打算在任何給定的一段時間來載入伺服器上儲存的資料量。  容量需求適用於; 僅限載入檔案作業系統和載入檔案應該在不同的磁碟陣列上。<br /><br />例如： 如果您打算 3 次每一天，從磁碟載入 100 GB 的資料，但一週，最後刪除資料檔案，則您需要儲存資料檔案的最小 2.1 TB。 我們建議您正在執行保守，也需取得詳細的 30%的儲存體的變異數和成長。  此範例中，2.73 TB 的儲存空間將會是更好。|  
|負載速率|每小時的資料將載入 PDW 位元組上限。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|這是估計值。 在計算此需求，假設檔案已在載入伺服器上，與其他載入條件會盡可能良好。<br /><br />例如： 不需要在資料可壓縮性，須因素，因為 dwloader 一律會將未壓縮的資料傳送至 PDW。 不是需要將納入資料型別轉換和目的地資料表的大小。|  
|網路|網路連線類型。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|判斷負載速率需求的最佳網路連線類型。<br /><br />例如： InfiniBand 或 10 Gbit 乙太網路會提供最佳的載入速度。 1 Gbit 乙太網路將會限制負載比率 360 gb 每小時或更少。|  
|I/O|每小時的讀取和寫入的位元組。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要載入資料，dwloader 必須讀取的所有資料從磁碟再將它傳送至 PDW。<br /><br />每個載入伺服器無法載入資料更應用裝置可以接收來自所有載入來源的資料。 若要節省成本，規劃的 I/O 讀取載入，因此不會超過設備的負載容量的容量。<br /><br />例如：<br />PDW 接收，並將資料載入至最大速率 1.8 TB 的每小時 1 機架應用裝置。 具有 2 個或多個機架應用裝置，最大負載比率會是每小時 3.6 TB。<br /><br />如果您打算同時從多個載入伺服器載入，每個載入伺服器的 I/O 需求會小於一部伺服器執行所有的載入時。<br /><br />例如： 一個來載入伺服器可以載入 1.8 TB 的最多每小時 1 機架應用裝置。 兩個載入伺服器可能每一個，同時載入 900 GB 每小時 1 機架應用裝置。 效率和最大輸送量，可以減少更高層級的並行存取。<br /><br />I/O 容量，採用到帳戶所有載入伺服器上發生的 I/O。 如果載入伺服器有其他的 I/O 流量，除了資料負載，例如 ETL 伺服器，從接收資料檔的 I/O 需求將會增加。<br /><br />壓縮的資料，對於的 I/O 需求而定的資料壓縮的速率。 dwloader 讀取壓縮的資料，然後再將它傳送至 PDW 它解壓縮。 高壓縮率，較少的資料載入伺服器必須從磁碟讀取。<br /><br />例如： 如果必要的負載速率是每小時，1.8 TB，而且資料會儲存在以 2:1 壓縮，來載入伺服器則載入伺服器只需要每小時而不是 1.8 TB 的磁碟讀取 900 GB。 3:1 壓縮比率表示載入伺服器需要每小時，從磁碟讀取 600 GB。|  
|CPU|插槽的數目。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|未壓縮的資料載入，dwloader 不需要大量 CPU 的應用程式。  最小需求，我們建議使用最近製造 2 通訊端伺服器。<br /><br />載入壓縮的資料，您必須以解壓縮資料再將它傳送至 PDW 足夠 CPU 能力。 dwloader 可以一次執行 10 個作用中的執行緒。 如果您打算同時載入 10 個壓縮的檔案，我們建議伺服器具有至少一個 10 核心 CPU 或兩個 6 核心 Cpu。|  
|RAM|GB 的記憶體中快取檔案期間，Windows 會載入。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|dwloader 載入伺服器上使用極少的 RAM。 效能，Windows 會使用記憶體來快取載入檔案之後從磁碟讀取。<br /><br />若要判斷 RAM 需求，請參閱 Windows Server 安裝和任何第 3 個合作對象應用程式的需求。 如果您不需要從其他來源的需求，我們建議至少 32 GB。<br /><br />壓縮的資料，更快速的 RAM 很有用，因為它將會加速解壓縮。|  
  
## <a name="see-also"></a>另請參閱  
[取得並設定載入伺服器](acquire-and-configure-loading-server.md)  
[dwloader 命令列載入器](dwloader.md)  
  
