---
title: 卸載修補程式
description: 卸載 Analytics Platform System 修補程式。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef6929aeb06c9472eb3ff210de016117a9636ded
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399758"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>卸載 Analytics Platform System 修補程式 
下列步驟說明如何卸載先前安裝的 Analytics Platform System 修補程式。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>必要條件  
若要執行這些步驟，您將需要：  
  
-   具有存取管理主控台來監視設備之許可權的分析平臺系統登入。  
  
-   要登入<em><appliance_domain></em> **HST01**節點的網域系統管理員帳戶。  
  
-   要卸載之修正程式的知識庫文章編號。  
  
## <a name="to-uninstall-a-sql-server-pdw-hotfix"></a><a name="HowToUninstallPDW"></a>卸載 SQL Server PDW 的修正程式  
  
1.  以網狀架構網域系統管理員身分登入<em><appliance_domain></em> **HST01**節點。  
  
2.  使用 [以系統管理員身分執行] 選項來開啟命令提示字元。  
  
3.  將目錄變更為要卸載之修正 `C:\PDWINST\Patches\<kbarticle>\media` *<kbarticle>* 程式的知識庫文章編號。  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  若要移除此修正程式，請執行下列命令。  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>另請參閱  
[下載並套用 Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[&#40;Analytics Platform System&#41;卸載 Microsoft Updates ](uninstall-microsoft-updates.md)  
[將 Analytics Platform System 修補程式套用 &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[軟體服務 &#40;Analytics Platform System&#41;](software-servicing.md)  
  
