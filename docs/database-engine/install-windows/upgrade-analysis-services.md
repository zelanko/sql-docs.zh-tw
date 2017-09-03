---
title: "升級 Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 07/17/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
caps.latest.revision: 79
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3b3ad4ecf62f3a30882720140f2f362007f8428b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="upgrade-analysis-services"></a>升級 Analysis Services
  Analysis Services 執行個體可以升級至相同伺服器模式的 SQL Server 版本，以利用目前版本中所採用的功能，如 [Analysis Services 的新功能](../../analysis-services/what-s-new-in-analysis-services.md)中所述。  
  
 您可以就地升級每個執行個體，相同硬體上執行的執行個體皆與其他執行個體無關。 但大部分的系統管理員會為應用程式測試選擇安裝新版本的新執行個體，然後再對新的伺服器傳輸實際執行的工作負載。 但是對於開發或測試伺服器而言，就地升級就可能會比較方便。  
  
 在升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之前，請檢閱下列文章：  

- [SQL Server 2017 版本資訊](../../sql-server/sql-server-2017-release-notes.md) 描述已知問題及因應措施。  
- [SQL Server 2016 版本資訊](../../sql-server/sql-server-2016-release-notes.md) 說明已知問題及因應措施。  
- [Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md) 總結了已停止、已被取代以及已變更的功能。 您應定期檢閱這些清單，評估對於您機型、指令碼或自訂程式碼之產品變更的影響。 一般而言，下一個主要版本的發行前版本會宣布功能轉換。  
  
## <a name="server-upgrade"></a>伺服器升級  
 升級伺服器與資料庫有兩種基本方法︰  
  
-   **就地升級** 會以 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 程式檔案取代現有的程式檔。 資料庫會保持在相同的位置。 程式資料夾會更新以反映新的名稱。  
  
-   **並存升級** 會建立新的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安裝，除非要同時升級硬體，否則通常會安裝在同一部電腦上。 這個方法會要求您將資料庫移至新的執行個體，然後再選擇性地解除安裝先前的版本，以釋出磁碟空間。  
  
 除非手動變更連結至指定伺服器的資料庫之相容性層級，否則這些層級會維持不變。  
  
### <a name="in-place-upgrade"></a>就地升級  
 您可以將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的現有執行個體升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] and, as part of the upgrade process, au的現有執行個體升級到matically migrate existing databases from the old instance 的現有執行個體升級到 the new instance. 由於這兩個版本之間的中繼資料和二進位資料是相容的，所以在您升級之後將會保留資料，而且不必手動移轉資料。  
  
 若要升級現有的執行個體，請執行安裝程式，並指定現有執行個體的名稱做為新執行個體的名稱。  
  
### <a name="side-by-side-upgrade"></a>並存升級  
  
-   備份所有資料庫，並確認每個資料庫皆可還原。 請參閱 [Backup and Restore of Analysis Services Databases](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)。  
  
-   找出報表、試算表或儀表板快照集的子集，以供日後用作為確認升級後伺服器作業的基礎。 請在可能的情況下收集效能測量，如此即可在升級的伺服器上針對相同的工作負載進行比較。  
  
-   安裝 Analysis Services 的新執行個體，選擇和您要取代的伺服器相同之伺服器模式 (表格式或多維度)。 請參閱 [Install Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)。  
  
     請遵循安裝後續工作，設定連接埠及新增伺服器管理員。 請參閱[後續安裝組態 &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)。  
  
-   附加或還原每個資料庫。  
  
-   執行 DBCC 以檢查資料庫完整性。 表格式模型會進行更徹底地檢查，會測試整個模型階層中是否有孤立的物件。 若是多維度模型，就只會檢查分割區索引。 請參閱 [Database Consistency Checker &#40;DBCC&#41; for Analysis Services 表格式和多維度資料庫](../../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md)。  
  
-   確認行為或計算是否有任何不良變更的測試報表、試算表與儀表板 您應會發現多維度與表格式工作負載的效能更佳。  
  
-   測試處理作業、更正任何登入或權限問題。 如果使用預設服務帳戶進行連線，新的服務會以不同的帳戶執行。 如需 Analysis Services 啟動帳戶的詳細資訊，請參閱[設定服務帳戶 &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)。  
  
-   在升級的伺服器上測試備份與還原作業，調整指令碼以使用新的伺服器名稱。  
  
## <a name="database-upgrade"></a>資料庫升級  
 在舊版 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中建立的資料庫會使用舊的資料庫相容性層級設定，在升級的伺服器上執行。 一般而言，您可以升級資料庫或模型到更高的相容性層級以存取新功能，但請注意，如此做會將您繫結至特定的伺服器版本。  
  
 若要升級資料庫，通常會升級 SQL Server Data Tools (SSDT) 中的模型，然後再將解決方案部署到已升級的伺服器執行個體。 請參閱 [下載 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) 以取得最新版本。  
  
 表格式與多維度資料庫走不同的版本路徑。 但多維度與表格式模型的相容性層級則皆為 1100。  如果功能變更只影響其中一個模式，則模式會上升至不同的費率。  
  
 因為背景的原因，下表摘要說明了相容性層級，但您應檢閱詳細主題以了解每個層級所提供的功能。  
  
||||  
|-|-|-|  
|表格式|1200|SQL Server 2016|  
|表格式|1103|SQL Server 2014|  
|表格式|1100|SQL Server 2012|  
|多維度|1100|SQL Server 2012 及更新版本|  
|多維度|1050|SQL Server 2005、2008、2008 R2|  
  
 如需詳細資訊，請參閱[多維度資料庫的相容性層級 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) 和 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。  
  
## <a name="tabular-model-upgrade-to-1200-compatibility-level"></a>表格式模型升級為 1200 相容性層級  
 表格式模型與資料庫從 SQL Server 2016 的獲益最多。 這個版本為表格式模型提供相容性層級 1200 的修訂版 DirectQuery 模式，其移除了混合模式而更為簡化，但加入了查詢陳述式以在設計階段擷取資料的子集，同時在後端資料庫中透過 DAX (非資料列權限) 提供資料列層級的安全性。  
  
 要升級的第二個原因，是模型內有新款表格式中繼資料建構。 新款相容性層級 1200 的表格式模型 (以該層級建立或升級至該層級)，使用物件定義的原生術語 (例如模型、資料表、關聯性與資料行) 來描述其主要元素。  
  
 若要升級表格式模型，請使用針對此版本所建置的 [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx) 版本，將 **相容性層級** 屬性變更為 **SQL Server 2016 RTM (1200)**。  
  
 請勿使用 SSMS、程式碼或指令碼來變更 **CompatibilityLevel**。 單獨使用時，變更屬性沒有任何作用。 而回應屬性的更新，會在 SSDT 中發生中繼資料轉換，之後會接著重新開啟專案。  
  
 一如往常，升級前請務必儲存一份模型備份，供萬一需要還原為升級前版本時之用。  
  
1.  在 [SSDT] > 方案總管中，以滑鼠右鍵按一下 **model.bim**，並選擇 [檢視程式碼]，認可會關閉該模型並於新的視窗中重新開啟 (程式碼視窗)。  
  
2.  以 XMLA 文件形式開啟該模型。 若是供比較的轉換後作業，請將內容複製到另一個檔案 (可以在 SSDT 中開啟新的 XML 檔案)。  
  
3.  以滑鼠右鍵按一下 **model.bim**，並將其變更回 [檢視表設計工具]。  
  
4.  將 **CompatibilityLevel** 設定為 **SQL Server 2016 RTM (1200)**。  
  
5.  此步驟無法還原，因此會要求您確認動作。 按一下 **[是]** 以繼續。 隨即會重新整理該專案。  
  
6.  以滑鼠右鍵按一下 **model.bim**，並將其變更回 [檢視程式碼]。  
  
     請注意，模型定義現已在 JSON 中，使用表格式中繼資料。  
  
 **中繼資料轉換**  
  
 比較轉換後及轉換前的中繼資料，會發現該中繼資料已轉換為 JSON，並已修剪掉多餘的定義。  
  
 模型會保留所有功能︰資料繫結、分割區配量、運算式、物件識別碼、物件名稱、描述、標題、翻譯以及註解，都會保持不變。 但如果您的程式碼或指令碼參考特定物件，則重寫程式碼時要移除對已不存在之物件的參考。 例如，1050 年或 1103 模型會有維度的區段，其位於 Cube 以外，而 1200 模型則會將資料表定義為單一物件。  
  
> [!NOTE]  
>  支援舊版 1050 與 1103 的表格式相容性層級，但已被取代。 SQL server 之後的一些版本中，將不再支援表格式模型轉換為多維度物件。 請參閱 [Deprecated Analysis Services Features in SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md) 以了解宣告。  
  
## <a name="post-upgrade-for-tabular-models-at-1200-compatibilitylevel"></a>1200 相容性層級的表格式模型之升級後作業  
 轉換模型之後，將會使用[表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)，而不是使用 XMLA 來撰寫資料庫作業的指令碼。 模型為 1200 時，在 SSMS 中自動產生 TMSL。 以表格式 1200 資料庫為標的之自訂程式碼，應使用 Microsoft.AnalysisServces.Tabular 命名空間中所定義的 API。 指令碼與程式碼必須從頭開始撰寫；沒有內建轉換的機制。 如需開始使用的說明，請參閱 [Analysis Services 開發人員文件](../../analysis-services/analysis-services-developer-documentation.md) 。  
  
 您也可對表格式模型加入下列功能 (只有相容性層級 1200 支援)︰  
  
-   DirectQuery 實作可在模型、多重資料來源、資料子集中，透過 DAX 支援資料列層級的安全性，供模型化及較簡單的組態之用。  
  
-   導出資料行  
  
-   顯示資料夾  
  
## <a name="upgrade-tabular-models-in-directquery-mode"></a>在 DirectQuery 模式下升級表格式模型  
 您無法為 DirectQuery 所設定的舊型表格式模型，執行就地升級。 DirectQuery 新實作的組態規模較小，因此不是所有設定都可移植。  
  
1.  在 SSDT 中，請關閉 **DirectQuery** 模式，讓該模型使用記憶體內部儲存體。 如需指示，請參閱 [啟用 DirectQuery 設計模式 (SSAS 表格式)](https://msdn.microsoft.com/library/hh270245.aspx) 。  
  
2.  將 **CompatibilityLevel** 設定為 SQL Server 2016 (RTM) 1200。  
  
3.  儲存並重新建立或部署該模型。  
  
4.  重新開啟 **DirectQuery** 。 請參閱 [DirectQuery for Tabular 1200 models](http://msdn.microsoft.com/library/4227977e-7368-4d45-b78f-24076882e7a8) 取得詳細指引。  
  
## <a name="see-also"></a>另請參閱  
 [DirectQuery 模式 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Analysis Services 的新功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [升級 Power Pivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [以多維度及資料採礦模式安裝 Analysis Services](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [使用安裝精靈升級為 SQL Server 2016 &#40;安裝程式&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

