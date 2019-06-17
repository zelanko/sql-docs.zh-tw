---
title: 軟體服務-Analytics Platform System |Microsoft Docs
description: 軟體服務 Analytics Platform System (APS)。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 444d7f29e7f65da7e5d98dde310b2c1f8ad8dd4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678392"
---
# <a name="software-servicing-in-analytics-platform-system"></a>Analytics Platform System 中的軟體維護
本節摘要說明服務的需求，Analytics Platform System appliance，包括 WSUS 和 Analytics Platform System hotfix 的軟體。  
  
## <a name="Basics"></a>軟體服務基本概念  
**WSUS:** Analytics Platform System appliance 必須設定為從 Windows Server Update Services (WSUS) 接收更新。 這些更新包括裝置軟體的重要變更。 設定之後，更新會自動安裝，並不需要實際操作的管理。 一般而言，設定 WSUS 更新期間[設定 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41; ](configure-windows-server-update-services-wsus.md)在新的應用裝置安裝期間執行的步驟。 如果沒有，則可以稍後再執行此組態步驟。 如需 WSUS 的資訊，請參閱[WSUS 網站指南](https://go.microsoft.com/fwlink/?LinkId=202417)。  
  
**Hotfix:** 此外，您可能需要套用 Analytics Platform System hotfix。 A *hotfix*建立特定的客戶，若要解決問題，Analytics Platform System 軟體的軟體更新。 每個 hotfix 是可執行檔安裝客戶特定問題的修正程式。 每個 hotfix 也會包含 Windows、 SQL Server 和 Analytics Platform System 的累積的所有先前發行的軟體更新。 如果您要安裝的 hotfix，Microsoft 支援服務將您提供的 hotfix 和指示。  
  
**更新的範圍：** 套用 Analytics Platform System hotfix 或 service pack 必須讓整個應用裝置離線。  
  
**SSIS 目的地配接器和用戶端工具：** 套用 hotfix 時，會包括 SSIS 目的地配接器 MSI 的變更，或用戶端工具 MSI，MSI 檔中將會更新**C:\PDWINST\ClientTools**目錄在控制節點上。 Hotfix 不會自動安裝元件，以從更新的 MSI 檔案。 若要更新這些元件，客戶必須解除安裝舊版本的元件，然後從更新的 MSI 檔案安裝新的版本。 解除安裝 hotfix 時，會包括 SSIS 目的地配接器 MSI 的變更，或用戶端工具 MSI，這些元件的 MSI 檔案，就會還原成先前的版本。 若要還原成先前版本的這些元件，必須先解除安裝現有的 （較新的） 版本的元件，客戶，並將其重新安裝較舊的版本，從已還原的 MSI 檔案中。  
  
## <a name="software-servicing-topics"></a>軟體服務主題  
下列主題說明如何管理軟體應用裝置上的服務：  
  
-   [下載並套用 Microsoft 更新&#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
  
-   [解除安裝 Microsoft 更新&#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
  
-   [套用 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [解除安裝 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
