---
title: 套用 Analytics Platform System Hotfix
description: 本文討論如何將修補程式套用至分析平臺系統軟體。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd62413ec8542aba9f3973d0e8483cb9c5c9128a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401368"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>套用 Analytics Platform System Hotfix
本文討論如何將修補程式套用至分析平臺系統軟體。  
  
## <a name="before-you-begin"></a>開始之前  
  
> [!WARNING]  
> 如果您的應用裝置或任何設備元件已關閉或處於故障狀態，請勿嘗試套用 Analytics Platform System 的修補程式。 在此情況下，請聯絡支援人員以尋求協助。  
  
> [!WARNING]  
> 當設備在使用中時，請勿套用 Analytics Platform System 的「應用程式」。 套用修補程式可能會導致應用裝置節點重新開機。 當設備不在使用中時，應在維護期間套用此修補程式。  
  
### <a name="prerequisites"></a>Prerequisites  
若要執行這些步驟，您將需要：  
  
-   具有許可權可存取管理主控台來監視設備狀態的分析平臺系統登入。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   瞭解用來連線至 _<domain_name>_ **-HST01**節點的網狀架構網域系統管理員帳戶。  
  
## <a name="to-apply-a-analytics-platform-system-hotfix"></a><a name="HowToInstallPDW"></a>套用 Analytics Platform System 的修復程式  
不同于 Microsoft updates，分析平臺系統軟體的修補程式不會透過 WSUS 來處理。 它們有不同的工作流程，並藉由執行修補程式套件來安裝。  
  
1.  **確認設備狀態指示器。**  
  
    1.  開啟管理主控台，並流覽至 [設備狀態] 頁面。 如需詳細資訊，請參閱[使用管理主控台監視設備 &#40;分析平臺系統&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  在您繼續進行下一個步驟之前，必須先解決所有的紅色或黃色指示器。 其中有幾個例外狀況：  
  
        -   如果發生磁片失敗，請使用 [管理主控台警示] 頁面，確認每個伺服器或 SAN 陣列內不會有一個以上的磁片失敗。 如果每個伺服器或 SAN 陣列內不會有一個以上的磁片失敗，您可以在修正磁片失敗之前繼續進行下一個步驟。 請務必聯絡 Microsoft 支援服務，儘快修正磁片失敗。  
  
        -   如果有非嚴重（黃色）磁片區錯誤（不在 C：\ 上）磁片磁碟機，您可以繼續進行下一個步驟，再解決磁片區錯誤。  
  
2.  **安裝 Analytics Platform System 的修補程式**  
  
    1.  以網域系統管理員身分登入 <*appliance_domain*> HST01 節點。  
  
    2.  使用 [以**系統管理員身分執行**] 選項來開啟命令提示字元。  
  
    3.  執行下列命令，以可*<HotfixPackageName>* 執行檔套件的名稱取代，並以適當的資訊取代其他預留位置專案 *<  >* 。  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  請遵循此修補程式套件所提供的步驟。  
  
## <a name="see-also"></a>另請參閱  
[下載並套用 Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[將 Microsoft Updates 卸載 &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[&#40;分析平臺系統&#41;卸載分析平臺系統修補程式](uninstall-analytics-platform-system-hotfixes.md)  
[軟體服務 &#40;分析平臺系統&#41;](software-servicing.md)  
  
