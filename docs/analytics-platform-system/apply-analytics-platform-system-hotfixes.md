---
title: "套用 Analytics Platform System Hotfix (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fca5eec9-86b8-4d20-b498-1678c367b5c8
caps.latest.revision: "25"
ms.openlocfilehash: 562d0ce41f5a1b12930fdedabd73214ddebd4e4e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="apply-analytics-platform-system-hotfixes"></a>套用分析平台系統的 Hotfix
本主題討論如何將 hotfix 套用到 Analytics Platform System 軟體。  
  
## <a name="before-you-begin"></a>開始之前  
  
> [!WARNING]  
> 請勿嘗試套用 Analytics Platform System hotfix，如果您的應用裝置或應用裝置中的任何元件是向下或在失敗狀態上方。 在此情況下，請連絡支援以尋求協助。  
  
> [!WARNING]  
> 設備正在使用時，請不要套用 Analytics Platform System hotfix。 套用 hotfix，可能會導致重新啟動的應用裝置節點。 未使用的應用裝置時，應套用 hotfix 維護期間。  
  
### <a name="prerequisites"></a>Prerequisites  
若要執行這些步驟，您必須：  
  
-   具有權限存取管理主控台來監視的應用裝置狀態 Analytics Platform System 登入。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   網狀架構網域系統管理員帳戶連接到的知識*< 網域名稱 >***-HST01**節點。  
  
## <a name="HowToInstallPDW"></a>若要套用 Analytics Platform System hotfix  
不同於 Microsoft 更新，Analytics Platform System 軟體 hotfix 不會處理透過 WSUS。 它們有不同的工作流程，而且會安裝執行 hotfix 封裝。  
  
1.  **請確認應用裝置狀態指標。**  
  
    1.  開啟管理主控台並巡覽至應用裝置狀態 頁面上。 如需詳細資訊，請參閱[使用系統管理員主控台 &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  在您繼續下一個步驟之前，必須先解決所有紅色或黃色指標。 這幾個例外狀況是：  
  
        -   如果發生磁碟失敗，使用 [系統管理主控台警示] 頁面，確認每個伺服器或 SAN 陣列內只能有一個磁碟故障。 每台伺服器或 SAN 陣列內有一個以上的磁碟失敗時，您可以繼續進行下一個步驟才能修復磁碟失敗。 請務必連絡 Microsoft 支援服務，以儘速修正磁碟失敗。  
  
        -   如果沒有非關鍵 （黃色） 磁碟區錯誤不是位於 C:\ 磁碟機，您可以繼續進行下一個步驟之前解決磁碟的磁碟區錯誤。  
  
2.  **Hotfix Analytics Platform System**  
  
    1.  登入 <*appliance_domain*>-HST01 節點，以網域系統管理員。  
  
    2.  使用**系統管理員身分執行**選項來開啟命令提示字元。  
  
    3.  執行下列命令，取代 *<HotfixPackageName>*  hotfix 可執行檔封裝，並取代的預留位置項目名稱取代*< >*適當的資訊。  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  表示 hotfix 封裝，請遵循的步驟。  
  
## <a name="see-also"></a>請參閱  
[下載並套用 Microsoft 更新 &#40;Analytics Platform System &#41;](download-and-apply-microsoft-updates.md)  
[解除安裝 Microsoft 更新 &#40;Analytics Platform System &#41;](uninstall-microsoft-updates.md)  
[分析平台系統 Hotfix &#40; 解除安裝Analytics Platform System &#41;](uninstall-analytics-platform-system-hotfixes.md)  
[軟體服務 &#40;Analytics Platform System &#41;](software-servicing.md)  
  
