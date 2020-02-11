---
title: Upgrade Advisor 總覽 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- SQL Server Upgrade Advisor, components
- tools [Upgrade Advisor]
- Upgrade Advisor [SQL Server], components
- components [Upgrade Advisor]
- Upgrade Advisor Analysis Wizard
- limitations [Upgrade Advisor]
- analyzing system [Upgrade Advisor]
- analyzing system [Upgrade Advisor], about analysis
ms.assetid: f5c56f63-4478-40af-abb9-642f58a0026c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c78630764a26bb8fe281446c1bb997f18d965db7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66091600"
---
# <a name="upgrade-advisor-overview"></a>Upgrade Advisor 概觀
  Upgrade Advisor 提供了一個中央主控台，可讓您分析 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 元件，並檢視包含有關分析結果資訊的報表。  
  
## <a name="how-upgrade-advisor-works"></a>Upgrade Advisor 如何運作  
 當您執行 Upgrade Advisor 時，Upgrade Advisor 開始頁面隨即顯示。 Upgrade Advisor 開始頁面是下列元件的啟動點：  
  
-   Upgrade Advisor 分析精靈  
  
-   Upgrade Advisor 報表檢視器  
  
-   Upgrade Advisor 說明  
  
 第一次使用 Upgrade Advisor 時，請執行 Upgrade Advisor 分析精靈來分析伺服器。 當 wizard 完成分析時，請按一下嚮導中的 [**啟動報表**]，或返回 Upgrade Advisor 起始頁。 如此，您就可以執行 Upgrade Advisor 報表檢視器來檢視報表。 此報表會提供一些資訊的連結，以便協助您解決已知的問題。  
  
## <a name="upgrade-advisor-analysis-wizard"></a>Upgrade Advisor 分析精靈  
 若要執行分析，請在 Upgrade Advisor 開始頁面上按一下 [**啟動 Upgrade Advisor 分析嚮導]** 。 Upgrade Advisor 分析精靈會蒐集有關您想要分析之電腦、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件和追蹤檔案的資訊。 在蒐集並確認所有資訊之後，Upgrade Advisor 分析精靈便分析 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件。  
  
> [!NOTE]  
>  每當您執行 Upgrade Advisor 分析精靈時，系統會產生不同的報表，而不會覆寫選取之元件的現有報表。 但是，報表檢視器只顯示最新的五個報表。  
  
 當 Upgrade Advisor 分析精靈完成分析時，它會針對您在分析中加入的每個元件建立一個 XML 檔案。 XML 檔案包含每個元件中發現的項目和問題。  
  
### <a name="what-upgrade-advisor-analyzes"></a>Upgrade Advisor 的分析內容  
 專用分析器會在每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的 Upgrade Advisor 內容中執行。 每個分析器的輸出都是該元件的 XML 報表。  
  
 Upgrade Advisor 會查詢下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件：  
  
-   資料庫伺服器 (《[!INCLUDE[ssDE](../../includes/ssde-md.md)] 線上叢書》中也稱為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 包含複寫、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式、全文檢索搜尋和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
> [!NOTE]  
>  在分析期間，每個分析器都會建立記錄檔。 您可以使用這些記錄檔針對分析進行疑難排解。 例如，如果 Upgrade Advisor 執行速度很慢，您就可以檢視記錄檔來判斷延遲的原因。  
  
### <a name="upgrade-advisor-limitations"></a>Upgrade Advisor 的限制  
 Upgrade Advisor 無法偵測可能會影響升級的所有問題。 例如，如果您已在使用者桌上型電腦上執行的用戶端應用程式中嵌入 SQL 程式碼，Upgrade Advisor 便無法分析這些應用程式。 針對這些項目，您仍然必須考慮上述問題並視需要升級、移轉或修改安裝中的資訊。  
  
 Upgrade Advisor 不會分析加密的預存程序、擴充預存程序中的程式碼，以及使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 以外語言撰寫的原始程式碼。  
  
## <a name="upgrade-advisor-report-viewer"></a>Upgrade Advisor 報表檢視器  
 若要查看 Upgrade Advisor 報表，請在 Upgrade Advisor 開始頁面上，按一下 [**啟動 Upgrade Advisor 報表檢視器]** 。 當 Upgrade Advisor 報表檢視器啟動時，它就會載入預設目錄中的報表。 如果 Upgrade Advisor 報表檢視器在預設目錄中找不到任何報表，它就不會顯示報表。 如果預設目錄中沒有任何報表，您可以執行 Upgrade Advisor 分析精靈來建立報表，或是從其他伺服器或子目錄載入現有的報表。  
  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Upgrade Advisor 不會覆寫現有報表。 但是，報表檢視器只顯示最新的五個報表。 若要查看先前的報表，請從 [**報表**] 下拉式清單方塊中選取報表。 時間戳記表示產生報表的日期和時間。  
  
 當 Upgrade Advisor 報表檢視器中載入 Upgrade Advisor 分析精靈的 XML 檔案時，它就會顯示每個元件的報表。 此報表包含所有您必須處理的已知問題，同時包括可偵測和無法偵測的問題。 針對每個問題，系統會顯示一個圖示 (指出重要性)、一個標籤 (告知您必須修正此問題的時間)，以及一則簡短描述。 當您展開問題時，將會看見更長的描述、問題詳細資料的連結和說明檔的連結。 每個問題的資訊都設計成提供足夠的資訊，可讓您修正問題。  
  
 大部分元件都具有無法偵測的問題。 若要查看這些問題，請展開元件的 [**其他升級問題**] 專案，然後按一下連結以在檔中查看有關問題的其他資訊。 如需有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 回溯相容性問題的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
