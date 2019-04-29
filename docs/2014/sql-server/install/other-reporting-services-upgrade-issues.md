---
title: 其他 Reporting Services 升級問題 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- command line setup [Reporting Services]
- Setup commands [Reporting Services]
- multivalued parameters [Reporting Services]
- WMI provider [Reporting Services]
- compile errors [Reporting Services]
- single-valued parameters [Reporting Services]
- data processing extensions [Reporting Services]
- report compilation errors [Reporting Services]
- authentication [Reporting Services]
ms.assetid: 42dd2f06-1de9-449e-ab9d-f4ef25f8b728
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: af30ed5d0e275353691e506dd49eeaebcea10d3e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011622"
---
# <a name="other-reporting-services-upgrade-issues"></a>其他 Reporting Services 升級問題
  本主題描述升級 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能時可能遇到的已知問題。 **Upgrade Advisor 不會偵測這些問題。** 如需詳細資訊，請參閱[SQL Server 2014 版本資訊](https://go.microsoft.com/fwlink/?LinkID=296445)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
|問題|描述|適用於|  
|-----------|-----------------|----------------|  
|SharePoint 伺服器陣列升級|請在伺服器陣列中所有其他 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件都已升級成 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之後，再升級 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 共用服務。<br /><br /> 若要升級[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在多節點 SharePoint 伺服器陣列[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，所有執行個體[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]增益集的 SharePoint 伺服器陣列中的必須先升級至[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]版本，才能升級[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]共用服務。<br /><br /> 如果 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 共用服務已經升級成 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，但伺服器陣列中的其他 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件仍然是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版，則報表轉譯將會失敗。<br /><br /> <br /><br /> 如需詳細資訊，請參閱＜ [SQL Server 2014 Reporting Services 提示、秘訣和疑難排解](https://go.microsoft.com/fwlink/?LinkID=391254)＞。|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|  
|並存安裝|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式無法與下列任一項並存執行：<br /><br /> 適用於 SharePoint 的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 共用服務<br /><br /> <br /><br /> 並存安裝會阻止[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式 Windows 服務啟動。 在 Windows 事件記錄檔中將會看見類似下面的錯誤訊息：<br /><br /> 描述：報表伺服器資料庫是無效的版本。<br /><br /> 描述：報表伺服器 [伺服器名稱] 無法連接到報表伺服器資料庫。|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 原生模式|  
|升級失敗的修復期間發生的錯誤|**問題：** 您嘗試升級失敗之後執行修復。 修復作業也失敗，而且您會在安裝記錄檔中看到類似以下的訊息：<br /><br /> `(01) 2011-10-27 12:23:15 Slp:` <br /> `(01) 2011-10-27 12:23:15 Slp: Exception type: System.Exception` <br /> `(01) 2011-10-27 12:23:15 Slp:     Message:`  <br /> `(01) 2011-10-27 12:23:15 Slp:         SQLPath element is missing` <br /> `(01) 2011-10-27 12:23:15 Slp:     Data:`  <br /> `(01) 2011-10-27 12:23:15 Slp:       SQL.Setup.FailureCategory = ConfigurationFailure`<br /><br /> 如需有關記錄檔的詳細資訊，請參閱 <<c0> [ 檢視與讀取 SQL Server Setup Log Files&lt](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。<br /><br /> **解決方案：** 您需要解除安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，並重新安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 無法再進行升級。|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|  
|只有儲存最後一個要求的互動性資訊。|在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，快照集會儲存互動式選擇的所有可能組合，例如鑽研資訊和切換選擇。 例如，您可以檢視某個報表的第五頁，但是透過追蹤切換的正確識別碼，以程式設計方式切換第一頁上的項目。<br /><br /> 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中，系統只會產生並儲存最後一個轉譯要求的互動性資訊。 因此，您無法檢視某個頁面，並以程式設計方式切換另一個頁面上的項目。 您只能切換目前報表頁面上的向下鑽研項目。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|轉譯和分頁已變更。|轉譯物件模型 (ROM) 中變更[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 目前已不再支援舊版轉譯物件模型。 此外，不支援從多執行緒轉譯延伸模組存取轉譯物件模型 (以及從多重執行緒切換內容)。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|重新設計的 CSV 匯出格式。|在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，當您將報表匯出成 CSV 檔案格式時，資料的格式化方式會保留該資料在報表頁面上顯示的方式。 若為矩陣資料區域，這會產生不方便匯入其他應用程式的資料格式。<br /><br /> 在此版本中，當您將報表匯出至 CSV 檔案，您可以選擇兩個支援的格式：預設模式和相容模式。 預設模式會針對 Excel 最佳化。 相容模式會針對協力廠商應用程式最佳化。<br /><br /> CSV 檔案的舊版格式已經無法使用。 不過，若為不使用矩陣資料區域的報表，您就可以使用相容模式來取得最接近舊版 CSV 檔案格式的檔案格式。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|使用頁首和頁尾中的條件式可見性進行彙總。|在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，不同的轉譯器會使用不同的規則來判斷哪些含有條件式可見性的項目要包含在報表頁面上。 例如，系統不會針對已列印報表中的隱藏項目執行彙總計算，但是會針對您使用瀏覽器或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 所檢視之報表中的隱藏項目進行計算。<br /><br /> 在這個版本中，所有轉譯器都會使用相同的規則集來判斷哪些項目位於頁面上。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|Excel 沒有公式支援。|在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，將 RDL 運算式轉譯成 Excel 公式的支援有所限制。 在這個版本中，當您將報表匯出至 Excel 時，RDL 運算式不會轉譯成 Excel 公式。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|重疊的項目。|在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，如果某個報表在報表設計介面上具有重疊的項目，則發行該報表時會產生一則警告 (「不是所有轉譯器都支援重疊報表項目。」)，但是報表項目會保留在設計介面上的原始位置。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中，當您檢視報表或將報表匯出至不支援重疊項目的轉譯器時，報表項目可能會移至正確的重疊界限。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|報表物件模型命名空間變更。|在  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，報表物件模型命名空間已經變更。 這個命名空間可讓您從自訂程式碼針對 `Fields`、`Parameters` 和 `ReportItems` 等全域集合進行唯讀存取。 如果現有的自訂程式碼明確使用舊版命名空間的完整參考，這項變更就是重大變更。<br /><br /> 建議您不要使用完整參考，從自訂程式碼存取內建集合。 透過不明確指定命名空間，自訂程式碼參考會解析成目前已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本的報表物件模型版本。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 的報表伺服器 Windows Management Instrumentation (WMI) 提供者。|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含 WMI 提供者，可讓您以程式設計方式設定報表伺服器執行的環境。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版包含全新版本的 WMI 提供者，可完全取代舊版。 這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 和 2005 版。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|在升級的報表伺服器上沒有重建服務主要名稱 (SPN)。|如果您針對報表伺服器 Web 服務建立了 SPN，請確認限制委派仍適用於升級的報表伺服器。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|您必須手動將自訂組件移至新的安裝資料夾。|Upgrade Advisor 無法偵測出自訂組件，而且如果您想要繼續在報表中使用自訂功能，就必須手動將它們移至新的安裝資料夾。<br /><br /> 如果這些組件安裝在報表伺服器安裝資料夾中，您就必須在升級完成之後，將它們移至新的安裝資料夾。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 升級問題&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
