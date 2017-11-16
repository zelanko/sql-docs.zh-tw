---
title: "設定磁碟空間使用量 (Power Pivot for SharePoint) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 201a3fda-f162-45d7-bf39-74dcb92fd0e6
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbd3fcbe7aa757ac95f225f7da01d7d54116e10b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="configure-disk-space-usage-power-pivot-for-sharepoint"></a>設定磁碟空間使用量 (PowerPivot for SharePoint)
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署會使用主機電腦的磁碟空間來快取 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫，讓重新載入更快速。 在記憶體中載入的每個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫都會先快取至磁碟中，因此稍後可以快速重新載入該資料庫來服務新的要求。 依預設， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 會使用所有可用磁碟空間來快取其資料庫，但是您可以藉由設定限制磁碟空間使用量的屬性來修改這個行為。  
  
 本主題說明如何設定磁碟空間使用量的限制。  
  
 本主題不會針對儲存在內容資料庫中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫 (內嵌在 Excel 活頁簿中)，提供磁碟空間管理的指導方針。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫可能很大，因此，請將新的需要放在伺服器陣列的儲存容量上。 此外，如果啟用版本設定，您可以在相同的內容資料庫中輕鬆擁有多個資料副本進一步增加內容儲存所需的磁碟空間量。 雖然 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫是磁碟管理的一個重要考量，但是它們無法獨立管理您儲存在 SharePoint 伺服器陣列中的其他內容。 當您的企業增加 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的用量時，您將需要更緊密監視磁碟空間。 您也可以在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板中追蹤 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿活動，並移除不再使用的活頁簿。  
  
## <a name="how-power-pivot-for-sharepoint-manages-cached-databases"></a>PowerPivot for SharePoint 如何管理快取資料庫  
 為了管理其快取， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務會定期執行背景作業，以清除內容庫中有較新版本的未使用或過期資料庫。 清除作業的目的是為了從記憶體中卸載非使用中的資料庫，以及從檔案系統中刪除未使用的快取資料庫。 清除作業供長期維護使用，以確保資料庫不會無限期地殘留在系統中。 在使用中的伺服器上，可能會因為記憶體對伺服器的壓力、SharePoint 中的資料庫刪除，或內容庫中有較新版的資料庫而更常移除資料庫。  
  
 雖然您無法排程清除作業，但是您可以設定執行下列操作的伺服器組態屬性來自訂快取檔案管理：  
  
-   設定快取所使用的磁碟空間量限制。  
  
-   指定達到磁碟空間上限時要刪除多少資料。  
  
## <a name="how-to-check-disk-space-usage"></a>如何檢查磁碟空間使用量  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝在 SharePoint 伺服器陣列中的應用程式伺服器上。 每個安裝都有一個包含 Backup 資料夾的資料目錄。 此 Backup 資料夾包含電腦上的 Analysis Services 執行個體所快取的所有資料檔。 根據預設，可以在以下路徑找到 Backup 資料夾：  
  
 `%drive%:\Program Files\Microsoft SQL Server\MSAS10_50.PowerPivot\OLAP\Backup\Sandboxes\<serviceApplicationName>`  
  
 若要檢查快取使用多少總磁碟空間，您必須檢查 Backup 資料夾的大小。 報告目前快取大小的管理中心沒有任何屬性。  
  
 [Backup] 資料夾會針對載入本機電腦上之記憶體中的任何 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫提供一般快取儲存。 如果您在伺服器陣列中定義多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，任何一個都可以使用本機伺服器載入並於隨後快取 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料。 資料載入和快取都是 Analysis Services 伺服器作業。 因此，總磁碟空間使用量會在 Analysis Services 執行個體層級的 Backup 資料夾上進行管理。 因此，限制磁碟空間使用量的組態設定會在 SharePoint 應用程式伺服器上執行的單一 SQL Server Analysis Services 執行個體上設定。  
  
 快取只包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫存放在單一父資料夾 ([Backup] 資料夾) 下的多個檔案中。 由於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫打算當作 Excel 活頁簿的內部資料使用，因此，資料庫名稱是以 GUID 為基礎，而非描述性的。 下的 GUID 資料夾**\<服務應用程式名稱 >**是父資料夾的[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]資料庫。 當 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫在伺服器上載入時，系統會針對每個資料庫建立其他資料夾。  
  
 由於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料可能會在伺服器陣列中的任何 Analysis Services 執行個體上載入，因此在伺服器陣列中的多部電腦上也可能會快取相同的資料。 這個作法是效能優先於磁碟空間使用量，但如果磁碟上已經有可用的資料，權衡取捨便是使用者可以更快速地存取資料。  
  
 若要立即減少磁碟空間耗用量，您可以關閉此服務，然後從 [Backup] 資料夾刪除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫。 手動刪除檔案是暫時的措施，因為下次查詢 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料時，會再次快取較新的資料庫複本。 永久性解決方案包括限制快取所使用的磁碟空間。  
  
 您可以在系統層級建立磁碟空間不足時通知您的電子郵件警示。 Microsoft System Center 包含電子郵件警示功能。 您也可以使用「檔案伺服器資源管理員」、「工作排程器」或 PowerShell 指令檔來設定警示。 下列連結提供實用的資訊來設定有關磁碟空間不足的通知：  
  
-   [檔案伺服器資源管理員的新功能](http://technet.microsoft.com/library/hh831746.aspx) (http://technet.microsoft.com/library/hh831746.aspx)。  
  
-   [File Server Resource Manager Step-by-Step Guide for Windows Server 2008 R2](http://go.microsoft.com/fwlink/?LinkID=204875) (Windows Server 2008 R2 的檔案伺服器資源管理員逐步指南) (http://go.microsoft.com/fwlink/?LinkID=204875)。  
  
-   [Setting low disk space alerts on Windows Server 2008](http://go.microsoft.com/fwlink/?LinkID=204870) (在 Windows Server 2008 上設定磁碟空間不足的警示) (http://go.microsoft.com/fwlink/?LinkID=204870)。  
  
## <a name="how-to-limit-the-amount-of-disk-space-used-for-storing-cached-files"></a>如何限制儲存快取檔案所使用的磁碟空間量  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 [管理伺服器上的服務]。  
  
2.  按一下 **[SQL Server Analysis Services]**。  
  
     請注意，限制是在實體伺服器上執行的 Analysis Services 執行個體上設定，而不是在服務應用程式層級設定。 使用本機 Analysis Services 執行個體的所有服務應用程式都遵從針對該執行個體設定的單一磁碟空間上限。  
  
3.  在 [磁碟使用量] 中，設定 [磁碟空間總計] 的值 (以 GB 為單位)，以便設定用於快取的空間量上限。 預設值為 0，這樣會允許 Analysis Services 使用所有可用的磁碟空間。  
  
4.  在 [磁碟使用量] 的 [Delete cached databases in last ‘n’ hours (刪除前 ‘n’ 個小時的快取資料庫)] 設定中，指定當磁碟空間達到上限時，上次使用的清空快取準則。  
  
     預設為 4 小時，這表示沒有任何活動達 4 小時以上的所有資料庫都會從檔案系統刪除。 非使用中但仍在記憶體中的資料庫會先遭到卸載，然後才從檔案系統刪除。  
  
## <a name="how-to-limit-how-long-a-database-is-kept-in-the-cache"></a>如何限制資料庫保留在快取中多久  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 [管理服務應用程式]。  
  
2.  按一下 [預設的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式] 開啟管理儀表板。  
  
3.  在 [動作]中，按一下 [設定服務應用程式設定]。  
  
4.  在 [磁碟快取] 區段中，您可以指定非使用中的資料庫存留在記憶體中多久，才能服務新要求 (預設為 48 小時)，以及存留在快取中多久 (預設為 120 小時)。  
  
     [將非使用中的資料庫保留在記憶體中] 會指定非使用中的資料庫要存留在記憶體中多久之後，才能服務該資料的新要求。 只要您要查詢使用中的資料庫，該資料庫就會永遠保留在記憶體中，但在資料庫不再處於使用中狀態時，系統會將該資料庫另外保留在記憶體中一段時間，以防有該資料的其他要求。  
  
     系統會先快取 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫，然後再載入記憶體中，因此，資料庫檔案會立即耗用磁碟空間。 不過，當資料庫處於使用中狀態 (而且持續 48 小時) 時，所有要求都會忽略快取資料庫，先導向至記憶體中的資料庫。 48 小時未有任何活動之後，就會從記憶體卸載檔案，但在本機 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器執行個體攔截該資料的新連接要求時可以快速重新載入存留在快取中的檔案。 對非使用中資料庫的連接要求是從快取 (而非內容庫) 服務的，因此可將對內容資料庫的影響降至最低。  
  
     請務必注意，內容庫是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫唯一的永久位置。 只有在內容庫中的資料庫與磁碟上的副本相同時，才會使用快取副本。  
  
     [將非使用中的資料庫保留在快取中] 會指定非使用中的資料庫要存留在檔案系統中多久之後，才能從記憶體卸載。 清除作業會使用這個設定來判斷要刪除的檔案。 未有任何活動達 168 小時 (記憶體中 48 小時，快取中 120 小時) 的所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫都會透過清除作業，從磁碟中刪除。  
  
5.  按一下 **[確定]** 儲存您的變更。  
  
## <a name="next-steps"></a>後續步驟  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝提供健全狀況規則，讓您可以在伺服器健全狀況、組態或可用性中偵測到問題時，採取更正動作。 這些規則中，有部分規則使用組態設定來決定觸發健全狀況規則的條件。 如果您積極地調整伺服器效能，可能也會想要檢閱這些設定，以確保預設值是對您系統最好的選擇。 如需詳細資訊，請參閱 [設定 Power Pivot 健全狀況規則](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [管理中心的 PowerPivot 伺服器管理和組態](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  

