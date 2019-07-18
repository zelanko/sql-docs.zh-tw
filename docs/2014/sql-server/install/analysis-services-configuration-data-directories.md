---
title: Analysis Services 組態-資料目錄 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ef732855-b7af-4f40-a619-5573c1c354bb
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 4ff1cd03eb260d892c22c36285fa07d912994510
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096804"
---
# <a name="analysis-services-configuration---data-directories"></a>Analysis Services 組態 - 資料目錄
  下表的預設目錄可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間由使用者設定。 存取這些檔案的權限會授與本機系統管理員，以及安裝期間建立及佈建的 SQLServerMSASUser$\<執行個體> 安全性群組成員。  
  
## <a name="uielement-list"></a>UIElement 清單  
  
|描述|預設目錄|建議|  
|-----------------|-----------------------|---------------------|  
|資料根目錄|C:\Program Files\Microsoft SQL Server\MSAS12。\<執行個體識別碼 > \OLAP\Data\|確保 \Program files\Microsoft SQL Server\ 資料夾受到有限權限。 在許多組態中，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 效能取決於資料目錄所在之儲存體的效能。 請將這個目錄放置於附加至系統的最高效能儲存體上。 若為容錯移轉叢集安裝，請確定資料目錄位於共用磁碟上。|  
|記錄檔目錄|C:\Program Files\Microsoft SQL Server\MSAS12。\<執行個體識別碼 > \OLAP\Log\|這是針對目錄[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]記錄檔，也包括了 FlightRecorder 記錄檔。 如果您增加了飛行記錄器持續時間，請確定記錄檔目錄具有足夠的空間。|  
|暫存目錄|C:\Program Files\Microsoft SQL Server\MSAS12。\<執行個體識別碼 > \OLAP\Temp\|置於高效能儲存體子系統的 Temp 目錄。|  
|備份目錄|C:\Program Files\Microsoft SQL Server\MSAS12。\<執行個體識別碼 > \OLAP\Backup\|這是針對目錄[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]預設備份檔案。 對於 PowerPivot for SharePoint 安裝來說，這也是 PowerPivot 系統服務快取 PowerPivot 資料檔案的位置。<br /><br /> 請確定已設定適當的權限來防止資料遺失，並且確定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務的使用者群組具有足夠的權限，可寫入備份目錄。 不支援針對備份目錄使用對應的磁碟機。|  
  
## <a name="notes"></a>注意  
  
-   部署在 SharePoint 伺服陣列上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會將應用程式檔案、資料檔案和屬性儲存在內容資料庫與服務應用程式資料庫中。  
  
-   將功能加入至現有的安裝時，您不能變更先前安裝之功能的位置，也不能指定新功能的位置。  
  
-   如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的目錄共用。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體內的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件也應該安裝在不同的目錄中。  
  
-   程式檔和資料檔案無法安裝在下列位置中：  
  
    -   抽取式磁碟機  
  
    -   使用壓縮的檔案系統  
  
    -   系統檔案所在的目錄  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的預設和具名執行個體的檔案位置](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
  
