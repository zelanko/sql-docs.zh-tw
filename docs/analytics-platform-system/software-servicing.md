---
title: 軟體服務
description: Analytics Platform System (AP) 的軟體服務。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4325dfa9c16edba12c2bba694b47c1b0875c7c6f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400308"
---
# <a name="software-servicing-in-analytics-platform-system"></a>分析平臺系統中的軟體服務
本節摘要說明 Analytics Platform System 設備的軟體服務需求，包括 WSUS 和 Analytics Platform System 的修補程式。  
  
## <a name="software-servicing-basics"></a><a name="Basics"></a>軟體服務基本概念  
**WSUS：** 您必須設定您的分析平臺系統裝置，以接收來自 Windows Server Update Services (WSUS) 的更新。 這些更新包括設備軟體的重要變更。 設定之後，將會自動安裝許多更新，且不需要實際操作管理。 WSUS 更新通常會在設定 [Windows Server Update Services &#40;wsus&#41; &#40;Analytics Platform System ](configure-windows-server-update-services-wsus.md) 期間進行設定，&#41;在新設備設定期間執行的步驟。 如果沒有，您可以稍後再執行此設定步驟。 如需 WSUS 的詳細資訊，請參閱 [wsus 網站指南](https://go.microsoft.com/fwlink/?LinkId=202417)。  
  
**修補程式：** 此外，您可能需要套用 Analytics Platform System 的修補程式。 修正 *程式* 是針對特定客戶所建立的軟體更新，可解決 Analytics Platform System 軟體的問題。 每個修復程式都是一個可執行檔，它會安裝客戶特定問題的修正程式。 每個修復程式也都包含所有先前已發行的 Windows、SQL Server 和 Analytics Platform System 軟體更新的累積。 如果您需要安裝修正程式，Microsoft 支援服務將提供您的修正程式和指示。  
  
**更新範圍：** 將修復程式或 service pack 套用至 Analytics Platform System 必須讓整個應用裝置離線。  
  
**SSIS 目的地介面卡和用戶端工具：** 套用包含 SSIS 目的地介面卡 MSI 或用戶端工具 MSI 變更的修正程式時，MSI 檔案將會在控制節點上的 **C:\PDWINST\ClientTools** 目錄中更新。 此修正程式並不會自動從更新的 MSI 檔案安裝元件。 若要更新這些元件，客戶必須卸載舊版本的元件，並從更新的 MSI 檔案安裝新的版本。 卸載包含 SSIS 目的地介面卡 MSI 或用戶端工具 MSI 變更的修正程式時，這些元件的 MSI 檔案將會還原為先前的版本。 若要將這些元件還原為先前的版本，客戶必須卸載現有 () 新版的元件，然後從還原的 MSI 檔案重新安裝較舊的版本。  
  
## <a name="software-servicing-topics"></a>軟體服務主題  
下列主題描述如何管理設備上的軟體服務：  
  
-   [下載並套用 Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
  
-   [&#40;Analytics Platform System&#41;卸載 Microsoft Updates ](uninstall-microsoft-updates.md)  
  
-   [將 Analytics Platform System 修補程式套用 &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [將 Analytics platform System 修補程式卸載 &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
