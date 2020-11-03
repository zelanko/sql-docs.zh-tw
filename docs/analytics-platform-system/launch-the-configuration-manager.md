---
title: 啟動 Configuration Manager
description: 針對 Analytics Platform System 設備啟動 Configuration Manager 工具的指示。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: be69331ec9f9daa091035d6ef21142c4f40d6a84
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235165"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>在 Analytics Platform System 中啟動 Configuration Manager
本主題提供啟動 Analytics Platform System 設備之 **Configuration Manager** 的指示。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>先決條件  
Analytics Platform System **Configuration Manager** 只能由設備網域系統管理員執行。 若要執行此工具，您需要設備網域系統管理員的密碼。 若要建立其他的 AP 系統管理員，請參閱 [建立 Ap 網域系統管理員 &#40;的 ap&#41;](create-an-aps-domain-administrator-aps.md)。  
  
## <a name="launch-the-configuration-manager-tool"></a><a name="Accessing"></a>啟動 Configuration Manager 工具  
若要執行 Configuration Manager，請使用遠端桌面連線到 PDW 控制項節點 ( **_PDW_region_ -CTL01** ) 節點，然後以 _appliance_domain_**\Administrator** 登入。 啟動 **Configuration Manager** 程式時，請使用 [ **以系統管理員身分執行** ] 選項，以確保使用您的系統管理員認證。  
  
#### <a name="to-launch-from-a-browser-window"></a>若要從瀏覽器視窗啟動  
  
1.  開啟瀏覽器並流覽至目錄 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` 。  
  
2.  以滑鼠右鍵按一下 `dwconfig.exe` ，然後按一下 [以 **系統管理員身分執行** ]。  
  
#### <a name="to-launch-from-a-command-prompt"></a>從命令提示字元啟動  
  
1.  在桌面上，開啟 [ **開始** ] 功能表，依序按一下 [程式]、[ **附屬** 應用 **程式** ]、[ **命令提示** 字元]，然後按一下 [以 **系統管理員身分執行** ]。  
  
2.  在命令提示字元中，輸入下列命令以變更目錄： `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"` 。  
  
3.  在命令提示字元處，輸入 `dwconfig.exe`。  
  
啟動 **Configuration Manager** 之後，您會看到左窗格中列出所有可用的功能。 本節的其餘部分將討論如何執行工具中可用的每個動作。  
  
若要關閉並結束 **Configuration Manager** ， **請按一下任何** 畫面右下角的 [結束]。  
  
![顯示裝置拓撲的 [Microsoft Analytics Platform System Configuration Manager] 對話方塊螢幕擷取畫面。](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>另請參閱  
[使用管理主控台 &#40;Analytics Platform System&#41;來監視設備 ](monitor-the-appliance-by-using-the-admin-console.md)  
  
