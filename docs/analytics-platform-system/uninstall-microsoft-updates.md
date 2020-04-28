---
title: 解除安裝 Microsoft Update
description: 卸載 Analytics Platform System （AP）中的 Microsoft updates。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a5ebe1ee911f7500505cdbd1962d28c35461a635
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399459"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>卸載 Analytics Platform System 中的 Microsoft updates
本文說明如何在 Analytics Platform System 設備上卸載先前安裝的 Microsoft update。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>Prerequisites  
若要執行這些步驟，您將需要：  
  
-   具有許可權可存取管理主控台來監視設備的分析平臺系統登入。  
  
-   瞭解用來登入<em> <Fabric Domain> </em> **-HST01**節點的網狀架構網域系統管理員帳戶。  
  
## <a name="to-uninstall-microsoft-updates"></a><a name="HowToUninstallMSFT"></a>卸載 Microsoft updates  
  
1.  以網狀架構網域<em> <Fabric Domain> </em>系統管理員身分登入 **-HST01**節點。  
  
2.  若要卸載已核准 WSUS 卸載的所有更新，請開啟 [命令提示字元] 視窗，然後輸入下列命令。 以適當的資訊取代預留位置專案 *<  >* 。  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱：
- [下載並套用 Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 
- [將分析平臺系統修補程式套用 &#40;分析平臺系統&#41;](apply-analytics-platform-system-hotfixes.md)  
- [&#40;分析平臺系統&#41;卸載分析平臺系統修補程式](uninstall-analytics-platform-system-hotfixes.md)  
- [軟體服務 &#40;分析平臺系統&#41;](software-servicing.md)  
  
