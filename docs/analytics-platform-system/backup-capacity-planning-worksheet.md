---
title: 備份伺服器容量規劃
description: 此容量規劃工作表可協助您判斷備份伺服器執行平行處理資料倉儲資料庫備份和還原作業的需求。 使用此功能來建立您的方案，以購買新的或布建現有的備份伺服器。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 57b036269dd4aeed91cf8af811bd2f24faecbb98
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171607"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>備份伺服器容量規劃工作表-平行處理資料倉儲
此容量規劃工作表可協助您判斷備份伺服器執行 SQL Server PDW 資料庫備份和還原作業的需求。 使用此功能來建立您的方案，以購買新的或布建現有的備份伺服器。

此工作表是[取得和設定備份伺服器](acquire-and-configure-backup-server.md)中指示的補充。

## <a name="capacity-planning-worksheet-for-backup-servers"></a>備份伺服器的容量規劃工作表

### <a name="notes"></a>注意

1.  此工作表適用于將執行 PDW 資料庫之備份和還原作業的伺服器。

2.  備份和還原 PDW 資料庫的唯一方式是使用備份資料庫和還原資料庫 SQL 命令。 不過，一旦備份資料位於備份伺服器上，它就會以一組 Windows 檔案的形式存在。 您可以使用傳統的 Windows 檔案型備份方法，將備份檔案從您的伺服器封存到另一個儲存位置。

### <a name="clipboard-icon-capacity-planning-worksheet"></a>![剪貼簿圖示](media/clipboard-icon.png "剪貼簿圖示")容量規劃工作表 

列印此工作表，並以您自己的需求填入。

|元件|需求|請在此資料行中填入您自己的需求|建議|
|-------------|---------------|--------------------------------------------------|-------------------|
|儲存體|您計畫在任何指定的時間儲存在備份伺服器上的最大位元組數。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要判斷儲存需求，請找出您計畫在任何指定時間儲存在備份伺服器上的資料量。<br /><br />備份資料會以壓縮格式儲存在備份伺服器上。 資料壓縮速率取決於您的資料特性。<br /><br />例如：作為粗略估計值，我們建議您估計相對於未壓縮資料大小的7:1 壓縮比率。 這假設至少有80% 的資料會儲存在叢集資料行存放區索引中。 例如，如果您在資料庫中有 700 GB 的未壓縮資料，而且儲存在叢集資料行存放區索引中，則您可以估計資料庫備份將需要 100 GB 的空間。<br /><br />如果您打算在備份伺服器上有多個資料庫備份複本，則需要將它們加以考慮。<br /><br />例如：如果您計畫備份10個資料庫，而每個資料庫都包含 5 TB 的未壓縮資料，則這些資料庫的大小結合為 50 TB。 如果您打算在一列中每天備份10個資料庫5天，則未壓縮的大小總計為 250 TB。 以7:1 壓縮比例進行分解時，您的備份伺服器上需要有 250/7 = 35.7 TB 的儲存體。 我們建議您保守，並取得大約30% 的額外容量，以考慮差異和成長。  在此範例中，46.6 TB 會較佳。|
|網路|網路連線類型。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|判斷可符合您的負載速率需求的最佳網路連線類型。<br /><br />例如：「不會」或 10Gbit Ethernet 會提供最佳的載入速度。 1Gbit Ethernet 會將負載速率限制為每小時 360 GB 或更少。|
|I/O|寫入的每小時位元組數。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|若要將備份寫入磁片，每小時 4 TB 寫入速度是最佳的。<br /><br />例如：對於可以寫入 50 MB/秒的磁片磁碟機，您需要至少24部磁片磁碟機，再加上更多鏡像或同位檢查。<br /><br />針對 i/o 容量，請考慮載入伺服器上發生的所有 i/o。 如果載入伺服器除了資料載入之外還有其他 i/o 流量（例如從 ETL 伺服器接收資料檔案），i/o 需求也會增加。|
|CPU|通訊端數目。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|接收和儲存備份檔案不是需要大量 CPU 的應用程式。  為最低需求，建議使用最近製造的2通訊端伺服器。|
|RAM|在載入期間允許 Windows 快取檔案的記憶體 GB。|![鉛筆圖示](media/pencil-icon.png "鉛筆圖示")|接收和儲存備份檔案需要載入伺服器上的 RAM 非常少。<br /><br />若要判斷 RAM 需求，請參閱您的 Windows Server 安裝和任何協力廠商應用程式需求。 如果您沒有其他來源的需求，建議您至少使用 32 GB。|

當您完成決定容量需求時，請回到[取得並設定載入伺服器](acquire-and-configure-loading-server.md)主題，以規劃您的購買。

## <a name="see-also"></a>另請參閱
[備份及載入硬體](backup-and-loading-hardware.md)

