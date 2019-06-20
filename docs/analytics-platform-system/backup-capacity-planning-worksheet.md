---
title: 備份伺服器容量計劃-Parallel Data Warehouse |Microsoft Docs
description: 這個容量規劃工作表可協助您決定備份的伺服器，以執行平行處理資料倉儲資料庫備份的需求和還原作業。 使用此選項來建立您的計劃購買新的或佈建現有備份伺服器。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 500bebab375a0d0b94032a1855af3844bc2e6fa7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63295054"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>備份伺服器容量規劃工作表-平行處理資料倉儲
這個容量規劃工作表可協助您決定備份的伺服器，以執行 SQL Server PDW 資料庫備份的需求和還原作業。 使用此選項來建立您的計劃購買新的或佈建現有備份伺服器。  
  
此工作表是中的指示補充[取得並設定備份伺服器](acquire-and-configure-backup-server.md)。  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>備份伺服器的容量規劃工作表  

### <a name="notes"></a>注意  
  
1.  此工作表適用於將會執行的 PDW 資料庫的備份和還原作業的伺服器。  
  
2.  備份和還原 PDW 資料庫的唯一方式是使用 備份資料庫 和 還原資料庫的 SQL 命令。 不過，您備份的伺服器上備份資料之後，它會存在為一組 Windows 檔案。 您可以封存的備份檔案從伺服器到另一個儲存體位置使用傳統 Windows 檔案型備份方法。  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![剪貼簿圖示](media/clipboard-icon.png "剪貼簿圖示")容量規劃工作表 
  
列印這張工作表，並填入您自己的需求。  
  
|元件|需求|在您自己的需求與此欄位填入|建議|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|儲存體|您計劃用於儲存備份的伺服器上，在任何給定的一段時間的最大位元組。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要判斷儲存體需求，找出您計劃用於儲存備份的伺服器上，在任何給定的一段時間的資料量。<br /><br />備份資料會儲存在備份伺服器，以壓縮格式。 資料壓縮率，取決於您資料的特性。<br /><br />例如：概略估計，我們建議估計 7:1 的壓縮比率，相對於您未壓縮的資料大小。 這是假設至少 80%的資料會儲存在叢集資料行存放區索引。 比方說，如果您的資料庫中有 700 GB 的未壓縮的資料，而且它會儲存在叢集資料行存放區索引，然後您可以估計的資料庫備份將會需要 100 GB。<br /><br />如果您打算備份的伺服器上有多個資料庫備份複本時，您需要為其帳戶。<br /><br />例如：如果您打算備份每個包含 5 TB 的未壓縮資料的 10 個資料庫，資料庫就會有 50 TB 的合併大的小時。 如果您打算備份這些 10 個資料庫每天 5 天的資料列中，未壓縮的大小總計會是 250 TB。 您將在 7:1 的壓縮比例，您將需要 250 / 7 = 35.7 TB 的儲存體備份的伺服器上。 我們建議您正在執行作保守估計，取得關於 30%的額外容量來考慮的變異數，而且成長。  在此範例中，46.6 TB 會是更好的。|  
|Network|網路連線類型。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|決定最佳的網路連線類型可符合負載速率需求。<br /><br />例如：InfiniBand 或 10Gbit 乙太網路會提供最佳的載入速度。 1Gbit 乙太網路會限制負載比率為 360 GB 每小時或更少。|  
|I/O|每小時寫入的位元組。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|寫入磁碟，每小時寫入速度是最佳的 4 TB 的備份。<br /><br />例如：可以寫入 50 MB/秒的磁碟機，您會想至少 24 的磁碟機，以及多個鏡像或同位檢查。<br /><br />I/O 容量考量帳戶所有載入伺服器上發生的 I/O。 如果載入伺服器有其他的 I/O 資料流，除了資料載入，例如從 ETL 伺服器，接收資料檔會增加的 I/O 需求。|  
|CPU|插槽的數目。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|接收與儲存備份的檔案不是需要大量 CPU 的應用程式。  最小的需求，我們建議使用最近製造 2 通訊端伺服器。|  
|RAM|GB 的記憶體中快取檔案期間，Windows 會載入。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|接收與儲存備份的檔案需要極少的 RAM，載入伺服器上。<br /><br />若要判斷的 RAM 需求，請參閱 Windows Server 安裝和任何第 3 個合作對象應用程式的需求。 如果您沒有從其他來源的需求，我們建議至少 32 GB。|  
  
當您完成判斷您的容量需求時，返回[取得並設定載入伺服器](acquire-and-configure-loading-server.md)計劃購買的主題。  
  
## <a name="see-also"></a>另請參閱  
[備份及載入硬體](backup-and-loading-hardware.md)  
  
