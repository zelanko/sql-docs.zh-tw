---
title: 設定時區-Analytics Platform System |Microsoft 文件
description: '[時區] 頁面可讓您設定 Analytics Platform System (APS) 應用裝置上的所有節點的時區。'
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6a17ef4e77f9703a285f1e232077582e4441f293
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544656"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>應用裝置的時區設定 Analytics Platform System
**時區**頁面可讓您設定 Analytics Platform System (APS) 應用裝置上的所有節點的時區。  
  
## <a name="to-set-the-time-zone"></a>若要設定時區  
  
1.  啟動 Configuration Manager。 如需詳細資訊，請參閱[啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  使用 停止應用裝置服務**服務狀態**Configuration Manager 中的頁面。 請參閱[PDW 服務狀態&#40;Analytics Platform System&#41; ](pdw-services-status.md)如需相關指示。  
  
3.  在左窗格的 Configuration Manager 中，按一下 **時區**。 選取所需的時區，從**時區**下拉式功能表。 根據您的位置，您也可以選擇以選取方塊旁的 **自動調整日光節約時間的時鐘**。  
  
4.  按一下**套用**以儲存變更。  
  
5.  重新啟動該應用裝置服務使用**服務狀態**Configuration Manager 中的頁面。 如果也想要變更權限，您可以應用裝置重新啟動之前執行。  
  
![DWConfig 應用裝置時間](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>另請參閱  
[啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
