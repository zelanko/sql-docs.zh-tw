---
title: "解除安裝 Microsoft 更新 (Analytics Platform System)"
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
ms.assetid: df61570a-210d-4154-822f-98acd721f075
caps.latest.revision: "19"
ms.openlocfilehash: 52bd212a753f4bb69c79d8b8e274664d2100cbee
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="uninstall-microsoft-updates"></a>解除安裝 Microsoft 更新
本主題描述如何解除安裝先前安裝的 Microsoft update，Analytics Platform System 應用裝置上。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>Prerequisites  
若要執行這些步驟，您必須：  
  
-   具有權限存取管理主控台來監視設備 Analytics Platform System 登入。  
  
-   網狀架構網域系統管理員帳戶登入的知識 *<Fabric Domain>*  **-HST01**節點。  
  
## <a name="HowToUninstallMSFT"></a>若要解除安裝 Microsoft 更新  
  
1.  登入 *<Fabric Domain>*  **-HST01**節點做為網狀架構網域系統管理員。  
  
2.  若要解除安裝所有的 WSUS，以解除安裝核准的更新，請開啟 [命令提示字元] 視窗並輸入下列命令。 取代的預留位置項目*< >*適當的資訊。  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="see-also"></a>請參閱  
[下載並套用 Microsoft 更新 &#40;Analytics Platform System &#41;](download-and-apply-microsoft-updates.md)  
[適用於分析的平台系統 Hotfix &#40;Analytics Platform System &#41;](apply-analytics-platform-system-hotfixes.md)  
[分析平台系統 Hotfix &#40; 解除安裝Analytics Platform System &#41;](uninstall-analytics-platform-system-hotfixes.md)  
[軟體服務 &#40;Analytics Platform System &#41;](software-servicing.md)  
  
