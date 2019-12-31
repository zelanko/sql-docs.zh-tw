---
title: 軟體服務
description: 分析平臺系統（AP）中的軟體服務。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4325dfa9c16edba12c2bba694b47c1b0875c7c6f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400308"
---
# <a name="software-servicing-in-analytics-platform-system"></a>分析平臺系統中的軟體服務
本節將摘要說明分析平臺系統裝置的軟體服務需求，包括 WSUS 和分析平臺系統修補程式。  
  
## <a name="Basics"></a>軟體服務基本概念  
**WSUS：** 您的分析平臺系統裝置必須設定為從 Windows Server Update Services （WSUS）接收更新。 這些更新包含設備軟體的重要變更。 設定好之後，將會自動安裝許多更新，而不需要實際操作管理。 通常，WSUS 更新會在設定[Windows Server Update Services &#40;wsus&#41; &#40;分析平臺系統](configure-windows-server-update-services-wsus.md)期間進行設定，&#41;步驟會在新設備安裝期間執行。 如果不是，則可以稍後執行此設定步驟。 如需 WSUS 的相關資訊，請參閱[wsus 網站指南](https://go.microsoft.com/fwlink/?LinkId=202417)。  
  
**修補程式：** 此外，您可能需要套用分析平臺系統修補程式。 「*修補程式*」是針對特定客戶所建立的軟體更新，可解決分析平臺系統軟體的問題。 每個修正程式都是可執行檔，它會安裝客戶特有問題的修正程式。 每個修復程式也包含所有先前發行的 Windows、SQL Server 和 Analytics Platform System 軟體更新的累積。 如果您需要安裝一個修補程式，Microsoft 支援服務將提供您有關此修補程式和指示。  
  
**更新範圍：** 將修補程式或 Service Pack 套用至分析平臺系統必須讓整個應用裝置離線。  
  
**SSIS 目的地介面卡和用戶端工具：** 套用包含 SSIS 目的地介面卡 MSI 或用戶端工具 MSI 變更的修補程式時，會在控制節點上的**C:\PDWINST\ClientTools**目錄中更新 MSI 檔案。 此修補程式不會自動從更新的 MSI 檔案安裝元件。 若要更新這些元件，客戶必須卸載舊版本的元件，並從更新的 MSI 檔案安裝新版本。 卸載包含 SSIS 目的地介面卡 MSI 或用戶端工具 MSI 變更的修補程式時，這些元件的 MSI 檔案將會還原為先前的版本。 若要將這些元件還原成先前的版本，客戶必須卸載元件的現有（較新版本），並從還原的 MSI 檔案重新安裝較舊的版本。  
  
## <a name="software-servicing-topics"></a>軟體服務主題  
下列主題說明如何管理設備上的軟體服務：  
  
-   [下載並套用 Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
  
-   [將 Microsoft Updates 卸載 &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
  
-   [將分析平臺系統修補程式套用 &#40;分析平臺系統&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [&#40;分析平臺系統&#41;卸載分析平臺系統修補程式](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
