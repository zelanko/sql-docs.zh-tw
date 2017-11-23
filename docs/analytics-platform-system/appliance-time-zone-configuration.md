---
title: "應用裝置的時區組態 (Analytics Platform System)"
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
ms.assetid: cea9eeb9-fe05-4e65-b229-539de02ab20a
caps.latest.revision: "18"
ms.openlocfilehash: 05cf2811dad14a6a7d53752893f363b061b86843
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-time-zone-configuration"></a>設定應用裝置時區
**時區**頁面可讓您設定 SQL Server PDW 應用裝置上的所有節點的時區。  
  
## <a name="to-set-the-time-zone"></a>若要設定時區  
  
1.  啟動 Configuration Manager。 如需詳細資訊，請參閱[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md).  
  
2.  使用 停止應用裝置服務**服務狀態**Configuration Manager 中的頁面。 請參閱[PDW 服務狀態 &#40;Analytics Platform System &#41;](pdw-services-status.md)如需相關指示。  
  
3.  在左窗格的 Configuration Manager 中，按一下 **時區**。 選取所需的時區，從**時區**下拉式功能表。 根據您的位置，您也可以選擇以選取方塊旁的 **自動調整日光節約時間的時鐘**。  
  
4.  按一下**套用**以儲存變更。  
  
5.  重新啟動該應用裝置服務使用**服務狀態**Configuration Manager 中的頁面。 如果也想要變更權限，您可以應用裝置重新啟動之前執行。  
  
![DWConfig 應用裝置時間](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>請參閱＜  
[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md)  
  
