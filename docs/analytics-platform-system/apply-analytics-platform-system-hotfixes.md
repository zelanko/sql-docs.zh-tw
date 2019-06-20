---
title: 套用 Analytics Platform System hotfix |Microsoft Docs
description: 這篇文章討論如何將 hotfix 套用到 Analytics Platform System 軟體。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b4b72017bb23ae44da9c5884f0ebf2a8b099fd3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63019043"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>套用 Analytics Platform System Hotfix
這篇文章討論如何將 hotfix 套用到 Analytics Platform System 軟體。  
  
## <a name="before-you-begin"></a>開始之前  
  
> [!WARNING]  
> 請勿嘗試套用 Analytics Platform System hotfix，如果您的設備或簽訂任何設備元件已關閉或處於容錯移轉狀態。 在此情況下，連絡支援服務尋求協助。  
  
> [!WARNING]  
> 設備在使用中時，請不要套用 Analytics Platform System hotfix。 套用 hotfix，可能會導致重新啟動的應用裝置節點。 未使用的應用裝置時，應該在維護期間套用 hotfix。  
  
### <a name="prerequisites"></a>先決條件  
若要執行這些步驟，您必須：  
  
-   具有權限存取管理主控台來監視設備狀態 Analytics Platform System 登入。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   網狀架構網域系統管理員帳戶連接到的知識 _< 網域名稱 >_ **-HST01**節點。  
  
## <a name="HowToInstallPDW"></a>套用 Analytics Platform System hotfix  
不同於 Microsoft updates，Analytics Platform System 軟體 hotfix 不會處理透過 WSUS。 它們有不同的工作流程，並會安裝在執行 hotfix 封裝。  
  
1.  **請確認應用裝置狀態指標。**  
  
    1.  開啟系統管理員主控台，然後瀏覽至 [應用裝置狀態] 頁面。 如需詳細資訊，請參閱 <<c0> [ 使用管理主控台來監視設備&#40;Analytics Platform System&#41;</c0>](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  在您繼續下一個步驟之前，必須先解決所有紅色或黃色指標。 這幾個例外狀況是：  
  
        -   如果發生磁碟失敗，使用 [系統管理員主控台中警示] 頁面來確認每個伺服器或 SAN 陣列內不超過一個磁碟故障。 如果有一個以上的磁碟失敗，每個伺服器或 SAN 陣列內，您可以繼續下一個步驟之前修正磁碟失敗。 請務必連絡 Microsoft 支援服務，以儘速修正磁碟失敗。  
  
        -   如果沒有不在 C:\ 磁碟機的非關鍵性 （黃色） 磁碟磁碟區錯誤，您可以繼續下一個步驟之前解決磁碟的磁碟區時發生錯誤。  
  
2.  **安裝 Analytics Platform System hotfix**  
  
    1.  登入 <*appliance_domain*>-HST01 網域系統管理員身分的節點。  
  
    2.  使用**系統管理員身分執行**選項來開啟命令提示字元。  
  
    3.  執行下列命令，取代 *<HotfixPackageName>* hotfix 可執行檔封裝，並取代的預留位置項目名稱取代 *< >* 適當的資訊。  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Hotfix 套件所提供，請遵循的步驟。  
  
## <a name="see-also"></a>另請參閱  
[下載並套用 Microsoft 更新&#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[解除安裝 Microsoft 更新&#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[解除安裝 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[軟體服務&#40;Analytics Platform System&#41;](software-servicing.md)  
  
