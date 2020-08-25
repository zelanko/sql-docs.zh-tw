---
title: 解除安裝 Microsoft Update
description: 卸載 Analytics Platform System (AP) 中的 Microsoft 更新。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a5ebe1ee911f7500505cdbd1962d28c35461a635
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399459"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>卸載 Analytics Platform System 中的 Microsoft updates
本文說明如何在 Analytics Platform System 設備上卸載先前安裝的 Microsoft update。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>必要條件  
若要執行這些步驟，您將需要：  
  
-   具有存取管理主控台來監視設備之許可權的分析平臺系統登入。  
  
-   登入 <em> <Fabric Domain> </em> **-HST01**節點的網狀架構網域系統管理員帳戶知識。  
  
## <a name="to-uninstall-microsoft-updates"></a><a name="HowToUninstallMSFT"></a>卸載 Microsoft update  
  
1.  以網狀 <em> <Fabric Domain> </em> 架構網域系統管理員身分登入 **-HST01**節點。  
  
2.  若要卸載核准 WSUS 卸載的所有更新，請開啟命令提示字元視窗，然後輸入下列命令。 使用適當的資訊來取代 *<  >* 的預留位置專案。  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱
- [下載並套用 Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 
- [將 Analytics Platform System 修補程式套用 &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
- [將 Analytics platform System 修補程式卸載 &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [軟體服務 &#40;Analytics Platform System&#41;](software-servicing.md)  
  
