---
title: 軟體服務 (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cec4d924-c88f-470c-84bb-0af3e21aabf1
caps.latest.revision: 33
ms.openlocfilehash: 8bddf00569ad4c5e5c78e801399b589a9f6d5f42
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="software-servicing"></a>軟體服務
本節摘要說明服務的需求，Analytics Platform System 應用裝置，包括 hotfix WSUS 與 Analytics Platform System 的軟體。  
  
## <a name="Basics"></a>軟體服務基本概念  
**WSUS:** Analytics Platform System 設備必須設定從 Windows Server Update Services (WSUS) 接收更新。 這些更新包括裝置軟體的重要變更。 這些設定之後，許多更新會自動安裝，並不需要實際操作的管理。 一般而言，設定 WSUS 更新期間[設定 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41; ](configure-windows-server-update-services-wsus.md)新的應用裝置安裝期間執行的步驟。 如果沒有，則可以稍後再執行此組態步驟。 如需 WSUS 的資訊，請參閱[WSUS 網站指南](http://go.microsoft.com/fwlink/?LinkId=202417)。  
  
**Hotfix:**此外，您可能需要套用 hotfix Analytics Platform System。 A *hotfix*是建立可解決的問題，Analytics Platform System 軟體與特定客戶的軟體更新。 可執行檔安裝客戶特定問題的修正每個的 hotfix。 每一個 hotfix 也會包含 Windows、 SQL Server 和 Analytics Platform System 的累積的所有先前發行的軟體更新。 如果您需要安裝的 hotfix，Microsoft 支援將您提供的 hotfix 和指示。  
  
**更新的範圍：** hotfix 或 service pack 套用到 Analytics Platform System 必須離線整個應用裝置。 也就是說，不會影響 PDW] 和 [HDInsight 區域。  
  
**SSIS 目的地配接器和用戶端工具：**套用 hotfix 時，包含 SSIS 目的地配接器 MSI 的變更，或用戶端工具 MSI，將在更新的 MSI 檔案**C:\PDWINST\ClientTools**在 [控制] 節點上的目錄。 Hotfix 不會自動安裝元件，以從更新的 MSI 檔案。 若要更新這些元件，客戶必須解除安裝舊版本的元件，然後從更新的 MSI 檔案安裝新版本。 解除安裝 hotfix 時，包含 SSIS 目的地配接器 MSI 的變更，或用戶端工具 MSI，這些元件的 MSI 檔案將還原為先前的版本。 若要還原到先前版本的這些元件，客戶必須解除安裝現有 （新） 版本的元件，然後重新安裝較舊的版本，從還原的 MSI 檔案。  
  
## <a name="software-servicing-topics"></a>軟體服務主題  
下列主題描述如何管理軟體應用裝置上的服務：  
  
-   [下載並套用 Microsoft 更新&#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
  
-   [解除安裝 Microsoft 更新&#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
  
-   [套用 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [解除安裝 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
