---
title: "啟動 Configuration Manager (Analytics Platform System)"
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
ms.assetid: b914ba9a-e4ec-4750-934a-c447fc8909e3
caps.latest.revision: "22"
ms.openlocfilehash: 2ead82cd226a585d261eac2779cacb72cd5edbb6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="launch-the-configuration-manager"></a>啟動 Configuration Manager
本主題提供指示來啟動**Configuration Manager** Analytics Platform System 應用裝置。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>Prerequisites  
Analytics Platform System**Configuration Manager**只能應用裝置的網域系統管理員身分執行。 若要執行這項工具，您需要應用裝置的網域系統管理員密碼。 若要建立 AP 的其他系統管理員，請參閱[建立 AP 網域系統管理員 &#40;APS &#41;](create-an-aps-domain-administrator-aps.md).  
  
## <a name="Accessing"></a>啟動組態管理員工具  
若要執行 組態管理員，使用遠端桌面連接至 PDW 控制節點 (***PDW_region*-CTL01**) 節點，然後登入為*appliance_domain* **\Administrator**。 啟動時**Configuration Manager**程式中，使用**系統管理員身分執行**選項，以確保會使用您的系統管理員認證。  
  
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
  
## <a name="see-also"></a>請參閱  
[使用系統管理員主控台 &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
