---
title: 啟動 Configuration Manager-Analytics Platform System |Microsoft Docs
description: 啟動 Analytics Platform System appliance 的 Configuration Manager 工具的指示。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 087360981a7c31de6980755cfee4f98f88f48a15
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502448"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>啟動 Analytics Platform System 中的 Configuration Manager
本主題提供指示來啟動**Configuration Manager** for Analytics Platform System appliance。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>先決條件  
Analytics Platform System**Configuration Manager**設備網域系統管理員，才可以執行。 若要執行這項工具，您需要設備網域系統管理員密碼。 若要建立其他的 APS 系統管理員，請參閱[建立 APS 網域系統管理員&#40;AP&#41;](create-an-aps-domain-administrator-aps.md)。  
  
## <a name="Accessing"></a>啟動組態管理員工具  
若要執行 Configuration Manager，請使用遠端桌面連接至 PDW 控制節點 (**_PDW_region_-CTL01**) 節點，然後登入為_appliance_domain_ **\Administrator**。 啟動時**Configuration Manager**程式中，使用**系統管理員身分執行**選項可確保使用您的系統管理員認證。  
  
#### <a name="to-launch-from-a-browser-window"></a>若要從瀏覽器視窗啟動  
  
1.  開啟瀏覽器並瀏覽至目錄`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
2.  以滑鼠右鍵按一下`dwconfig.exe`，然後按一下 **系統管理員身分執行**。  
  
#### <a name="to-launch-from-a-command-prompt"></a>若要從命令提示字元啟動  
  
1.  在桌面上，開啟**開始**功能表上，按一下**程式**，按一下 **附屬應用程式**，以滑鼠右鍵按一下**命令提示字元**，然後按一下**系統管理員身分執行**。  
  
2.  在命令提示字元中，輸入下列命令，將目錄變更為： `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`。  
  
3.  在命令提示字元中，輸入`dwconfig.exe`。  
  
在後**Configuration Manager**會啟動，您會看到列在左窗格中的所有可用的功能。 本節的其餘部分將討論如何執行此工具的每個動作。  
  
若要關閉並結束**Configuration Manager**，按一下**結束**任何畫面右下角。  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>另請參閱  
[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
