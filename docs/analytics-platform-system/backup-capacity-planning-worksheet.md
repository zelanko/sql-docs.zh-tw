---
title: 備份伺服器容量規劃工作表 (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: 這個容量規劃工作表可協助您判斷執行 SQL Server PDW 資料庫備份的備份伺服器的需求和還原作業。
ms.date: 01/05/2017
ms.topic: article
ms.assetid: 36294bf6-6dde-481f-a190-d4382b04c030
caps.latest.revision: 6
ms.openlocfilehash: 1548d284f78043e5f878bafe9922480fe762dbfe
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="backup-server-capacity-planning-worksheet"></a>備份伺服器容量規劃工作表
這個容量規劃工作表可協助您判斷執行 SQL Server PDW 資料庫備份的備份伺服器的需求和還原作業。 使用此選項來建立您的計劃購買新的或佈建現有備份伺服器。  
  
此工作表是中的指示的補充[取得和設定備份伺服器](acquire-and-configure-backup-server.md)。  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>備份伺服器的容量規劃工作表  

### <a name="notes"></a>注意  
  
1.  此工作表適用於將執行 PDW 資料庫的備份和還原作業的伺服器。  
  
2.  備份和還原 PDW 資料庫的唯一方式是使用 備份資料庫和還原資料庫的 SQL 命令。 不過，一旦您備份的伺服器上備份資料，它會存在為一組 Windows 檔案。 您可以封存的備份檔案從伺服器到另一個儲存位置使用傳統的 Windows 檔案型備份方法。  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![剪貼簿圖示](media/clipboard-icon.png "剪貼簿圖示")容量規劃工作表 
  
列印此工作表，並填入您自己的需求。  
  
|元件|需求|在您自己的需求與此資料行填滿|建議|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|儲存空間|您計劃在任何給定的一段時間備份伺服器上儲存的位元組上限。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要判斷儲存體需求，找出您打算在任何給定的一段時間備份伺服器上儲存的資料量。<br /><br />備份資料會儲存在壓縮格式的備份伺服器上。 資料壓縮率會取決於您資料的特性。<br /><br />例如： 概略估計，我們建議估計相對於您未壓縮的資料大小的 7:1 壓縮比率。 這是假設至少 80%的資料會儲存在叢集資料行存放區索引。 比方說，如果您在資料庫中有 700 GB 的未壓縮的資料會儲存在叢集資料行存放區索引，然後您可以估計的資料庫備份將會需要 100 GB。<br /><br />如果您打算備份的伺服器上有多個複本的資料庫備份，您需要為其帳戶。<br /><br />例如： 如果您計劃將 10 個各自包含 5TB 的未壓縮資料的資料庫備份，資料庫會具有 50TB 合併的大小。 如果您計劃備份這些 10 個資料庫每天 5 天的資料列中，未壓縮的大小總計會是 250 TB。 考量 redo 7:1 壓縮比率，您將需要 250 / 7 = 35.7 TB 的儲存體備份伺服器上。 我們建議您正在執行保守和取得有關 30%的變異數，並增加額外的容量。  在此範例中，會更好 46.6 TB。|  
|網路|網路連線類型。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|決定最佳的網路連線類型符合負載速率需求。<br /><br />例如： InfiniBand 或 10Gbit 乙太網路會提供最佳的載入速度。 1Gbit 乙太網路將會限制負載比率 360 gb 每小時或更少。|  
|I/O|每小時的寫入位元組。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|供寫入至磁碟，每小時寫入速度是最佳的 4 TB 的備份。<br /><br />例如： 可以撰寫 50 MB/秒，您會想至少 24 的磁碟機的磁碟機，再加上多個鏡像或同位檢查。<br /><br />I/O 容量，採用到帳戶所有載入伺服器上發生的 I/O。 如果載入伺服器有其他的 I/O 流量，除了資料負載，例如 ETL 伺服器，從接收資料檔的 I/O 需求將會增加。|  
|CPU|插槽的數目。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|接收並儲存備份檔案不是需要大量 CPU 的應用程式。  最小需求，我們建議使用最近製造 2 通訊端伺服器。|  
|RAM|GB 的記憶體中快取檔案期間，Windows 會載入。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|接收並儲存備份檔案需要極少的 RAM，載入伺服器上。<br /><br />若要判斷 RAM 需求，請參閱 Windows Server 安裝和任何第 3 個合作對象應用程式的需求。 如果您不需要從其他來源的需求，我們建議至少 32 GB。|  
  
當您完成判斷您的容量需求時，返回[取得和設定載入伺服器](acquire-and-configure-loading-server.md)規劃購買程序主題。  
  
## <a name="see-also"></a>另請參閱  
[備份及載入硬體](backup-and-loading-hardware.md)  
  
