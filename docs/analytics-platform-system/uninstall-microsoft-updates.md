---
title: 解除安裝 Microsoft 更新-Analytics Platform System |Microsoft Docs 」
description: 解除安裝 Analytics Platform System (APS) 的 Microsoft 更新。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4739d05b1878c8b7fc9f66f2e0b8145ff1044e54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63243829"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>解除安裝 Analytics Platform System 中的 Microsoft 更新
本文說明如何解除安裝先前安裝的 Microsoft update，Analytics Platform System 應用裝置上。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>先決條件  
若要執行這些步驟，您必須：  
  
-   具有權限存取管理主控台來監視設備 Analytics Platform System 登入。  
  
-   網狀架構網域系統管理員帳戶來登入的知識<em> <Fabric Domain> </em> **-HST01**節點。  
  
## <a name="HowToUninstallMSFT"></a>若要解除安裝 Microsoft 更新  
  
1.  登入<em> <Fabric Domain> </em> **-HST01**節點為網狀架構網域系統管理員。  
  
2.  若要解除安裝所有核准解除安裝 wsus 的更新，請開啟 [命令提示字元] 視窗並輸入下列命令。 取代預留位置項目 *< >* 適當的資訊。  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱：
- [下載並套用 Microsoft 更新&#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 
- [套用 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
- [解除安裝 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [軟體服務&#40;Analytics Platform System&#41;](software-servicing.md)  
  
