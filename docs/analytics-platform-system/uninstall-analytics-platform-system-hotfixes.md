---
title: 解除安裝中的 Analytics Platform System hotfix |Microsoft Docs
description: 解除安裝 Analytics Platform System hotfix。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5507eae7bb2f8a5ce138223a031ac4946d9f0030
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62675667"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>解除安裝 Analytics Platform System hotfix 
下列步驟說明如何解除安裝先前安裝的 Analytics Platform System hotfix。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>先決條件  
若要執行這些步驟，您必須：  
  
-   具有權限存取管理主控台來監視設備 Analytics Platform System 登入。  
  
-   網域系統管理員帳戶登入<em>< appliance_domain ></em>**-HST01**節點。  
  
-   知識庫文章編號，為了讓 hotfix 解除安裝。  
  
## <a name="HowToUninstallPDW"></a>若要解除安裝 SQL Server PDW hotfix  
  
1.  登入<em>< appliance_domain ></em>**-HST01**節點為網狀架構網域系統管理員。  
  
2.  使用 [執行為系統管理員] 選項開啟命令提示字元。  
  
3.  將目錄變更為`C:\PDWINST\Patches\<kbarticle>\media`何處*<kbarticle>* 解除安裝此 hotfix 的知識庫文件編號。  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  若要移除此 hotfix，請執行下列命令。  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>另請參閱  
[下載並套用 Microsoft 更新&#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[解除安裝 Microsoft 更新&#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[套用 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[軟體服務&#40;Analytics Platform System&#41;](software-servicing.md)  
  
