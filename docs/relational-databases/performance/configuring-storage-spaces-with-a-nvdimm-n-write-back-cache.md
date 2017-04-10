---
title: "設定具有 NVDIMM-N 回寫式快取的儲存空間 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-non-specified"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 861862fa-9900-4ec0-9494-9874ef52ce65
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# 設定具有 NVDIMM-N 回寫式快取的儲存空間
  Windows Server 2016 支援 NVDIMM-N 裝置，以大幅加快輸入/輸出 (I/O) 作業的速度。 這類裝置一個吸引人的用法是作為回寫式快取，以取得低寫入延遲。 本主題討論如何設定具有鏡像 NVDIMM N 回寫式快取的鏡像儲存空間，以作為虛擬磁碟機，來儲存 SQL Server 交易記錄。 如果您也想使用它來儲存資料表或其他資料，您可以將更多磁碟加入存放集區，或建立多個集區 (若隔離很重要)。  
  
 若要檢視使用這項技術的 Channel 9 影片，請參閱 [Using Non-volatile Memory (NVDIMM-N) as Block Storage in Windows Server 2016](https://channel9.msdn.com/Events/Build/2016/P466) (在 Windows Server 2016 中使用靜態記憶體 (NVDIMM-N) 作為區塊存放裝置)。  
  
## 識別正確的磁碟  
 在 Windows Server 2016 中設定儲存空間，特別是使用進階功能 (例如回寫式快取)，最簡單的方法是透過 PowerShell。 第一個步驟是識別應該作為儲存空間集區一部分的磁碟，此集區會是建立虛擬磁碟的來源。 NVDIMM-N 的媒體類型和匯流排類型為 SCM (儲存類別記憶體)，可透過 Get-PhysicalDisk PowerShell Cmdlet 來查詢。  
  
```  
Get-PhysicalDisk | Select FriendlyName, MediaType, BusType  
```  
  
 ![Get-PhysicalDisk](../../relational-databases/performance/media/get-physicaldisk.png "Get-PhysicalDisk")  
  
> [!NOTE]  
>  使用 NVDIMM-N 裝置時，您不再需要明確選取可作為回寫式快取目標的裝置。  
  
 為了建立具有鏡像回寫式快取的鏡像虛擬磁碟，至少需要 2 部 NVDIMM-N 和 2 個其他磁碟。 將所需的實體磁碟指派給變數再建立集區可簡化程序。  
  
```  
$pd =  Get-PhysicalDisk | Select FriendlyName, MediaType, BusType | WHere-Object {$_.FriendlyName -like 'MK0*' -or $_.FriendlyName -like '2c80*'}  
```  
  
 此螢幕擷取畫面顯示 $pd 變數，以及使用下列 PowerShell Cmdlet 傳回之指派給該變數的 2 個 SSD 和 2 部 NVDIMM-N。  
  
```  
$pd | Select FriendlyName, MediaType, BusType  
```  
  
 ![Select FriendlyName](../../relational-databases/performance/media/select-friendlyname.png "Select FriendlyName")  
  
## 建立存放集區  
 您可以透過包含 PhysicalDisks 的 $pd 變數，輕鬆地使用 New-StoragePool PowerShell Cmdlet 建立存放集區。  
  
```  
New-StoragePool –StorageSubSystemFriendlyName “Windows Storage*” –FriendlyName NVDIMM_Pool –PhysicalDisks $pd  
```  
  
 ![New-StoragePool](../../relational-databases/performance/media/new-storagepool.png "New-StoragePool")  
  
## 建立虛擬磁碟和磁碟區  
 建立集區之後，下一個步驟是對虛擬磁碟進行切割及格式化。 在本例中，只會建立一個虛擬磁碟，而且可以使用 New-Volume PowerShell Cmdlet 簡化此程序：  
  
```  
New-Volume –StoragePool (Get-StoragePool –FriendlyName NVDIMM_Pool) –FriendlyName Log_Space –Size 300GB –FileSystem NTFS –AccessPath S: -ResiliencySettingName Mirror  
```  
  
 ![New-Volume](../../relational-databases/performance/media/new-volume.png "New-Volume")  
  
 虛擬磁碟已建立、初始化並以 NTFS 格式化。 下列螢幕擷取畫面顯示它具有 300 GB 的大小與 1 GB 的寫入快取大小，並將裝載於 NVDIMM-N。  
  
 ![Get-VirtualDisk](../../relational-databases/performance/media/get-virtualdisk.png "Get-VirtualDisk")  
  
 您現在可以檢視伺服器中顯示的這個新磁碟區。 您現在可以使用此磁碟機來儲存 SQL Server 交易記錄。  
  
 ![Log_Space Drive](../../relational-databases/performance/media/log-space-drive.png "Log_Space Drive")  
  
## 另請參閱  
 [Windows 10 中的 Windows 儲存空間](http://windows.microsoft.com/en-us/windows-10/storage-spaces-windows-10)   
 [Windows 2012 R2 中的 Windows 儲存空間](https://technet.microsoft.com/en-us/library/hh831739.aspx)   
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [檢視或變更資料及記錄檔的預設位置 &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view or change the default locations for data and log files.md)  
  
  