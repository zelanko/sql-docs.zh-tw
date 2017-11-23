---
title: "解除安裝 Analytics Platform System Hotfix (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9ab596d-3f5a-48e2-bce7-c9be99b8c23b
caps.latest.revision: "21"
ms.openlocfilehash: 04740eeccc1b7837c278ce0041cc1e6f78fd4c60
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>解除安裝 Analytics Platform System Hotfix
下列步驟說明如何解除安裝先前安裝的 Analytics Platform System hotfix。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>必要條件  
若要執行這些步驟，您必須：  
  
-   具有權限存取管理主控台來監視設備 Analytics Platform System 登入。  
  
-   網域系統管理員帳戶登入*< appliance_domain >***-HST01**節點。  
  
-   知識庫文章編號，為了讓 hotfix 以解除安裝。  
  
## <a name="HowToUninstallPDW"></a>若要解除安裝 SQL Server PDW hotfix  
  
1.  登入*< appliance_domain >***-HST01**節點做為網狀架構網域系統管理員。  
  
2.  使用 執行做為系統管理員的選項來開啟命令提示字元。  
  
3.  將目錄變更為`C:\PDWINST\Patches\<kbarticle>\media`其中 *<kbarticle>* 解除安裝此 hotfix 的知識庫文件編號。  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  若要移除這個 hotfix，執行下列命令。  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>請參閱＜  
[下載並套用 Microsoft 更新 &#40;Analytics Platform System &#41;](download-and-apply-microsoft-updates.md)  
[解除安裝 Microsoft 更新 &#40;Analytics Platform System &#41;](uninstall-microsoft-updates.md)  
[適用於分析的平台系統 Hotfix &#40;Analytics Platform System &#41;](apply-analytics-platform-system-hotfixes.md)  
[軟體服務 &#40;Analytics Platform System &#41;](software-servicing.md)  
  
