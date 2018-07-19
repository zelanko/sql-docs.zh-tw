---
title: 啟動 Configuration Manager-Analytics Platform System |Microsoft 文件
description: 啟動組態管理員工具，Analytics Platform System 應用裝置的指示。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d2e7a726386aa64d04f87f30cd22328900b1e5cd
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544780"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>啟動 Configuration Manager 中 Analytics Platform System
本主題提供指示來啟動**Configuration Manager** Analytics Platform System 應用裝置。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>필수 구성 요소  
Analytics Platform System**Configuration Manager**只能應用裝置的網域系統管理員身分執行。 若要執行這項工具，您需要應用裝置的網域系統管理員密碼。 若要建立 AP 的其他系統管理員，請參閱[建立 AP 網域系統管理員&#40;AP&#41;](create-an-aps-domain-administrator-aps.md)。  
  
## <a name="Accessing"></a>啟動組態管理員工具  
若要執行 組態管理員，使用遠端桌面連接至 PDW 控制節點 (***PDW_region *-CTL01**) 節點，然後登入為 * appliance_domain ***\Administrator**。 啟動時**Configuration Manager**程式中，使用**系統管理員身分執行**選項，以確保會使用您的系統管理員認證。  
  
#### <a name="to-launch-from-a-browser-window"></a>若要從瀏覽器視窗中啟動  
  
1.  開啟瀏覽器並瀏覽至目錄`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
2.  以滑鼠右鍵按一下`dwconfig.exe`，然後按一下 **系統管理員身分執行**。  
  
#### <a name="to-launch-from-a-command-prompt"></a>若要從命令提示字元啟動  
  
1.  在桌面上，開啟**啟動**功能表上，按一下 **程式**，按一下 **附屬應用程式**，以滑鼠右鍵按一下**命令提示字元**然後按一下  **系統管理員身分執行**。  
  
2.  在命令提示字元中，輸入下列命令以變更目錄： `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`。  
  
3.  在命令提示字元中，輸入`dwconfig.exe`。  
  
之後**Configuration Manager**會啟動，您會看到所有可用的左窗格中所列的功能。 本節的其餘部分將討論如何執行此工具的每個動作。  
  
若要關閉並結束**Configuration Manager**，按一下 **結束**任何畫面右下角。  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>另請參閱  
[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
