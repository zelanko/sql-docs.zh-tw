---
title: 設定時區-Analytics Platform System |Microsoft Docs
description: '[時區] 頁面可讓您設定 Analytics Platform System (APS) 設備上的所有節點的時區。'
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f9997ed26cea5c63d69a7be84b25c247add9b692
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961446"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>設備時區設定 Analytics Platform System
**時區**頁面可讓您設定 Analytics Platform System (APS) 設備上的所有節點的時區。  
  
## <a name="to-set-the-time-zone"></a>若要設定時區  
  
1.  啟動組態管理員。 如需詳細資訊，請參閱 <<c0> [ 啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。</c0>  
  
2.  使用停止設備服務**Services 狀態**頁面在 Configuration Manager 中。 請參閱[PDW 服務狀態&#40;Analytics Platform System&#41; ](pdw-services-status.md)如需相關指示。  
  
3.  在左窗格的 Configuration Manager 中，按一下**時區**。 選取從所需的時區**時區**下拉式選單。 根據您的位置，您也可以選擇以選取方塊旁**自動調整日光節約時間的時鐘**。  
  
4.  按一下 **套用**以儲存變更。  
  
5.  使用重新啟動的應用裝置的服務**Services 狀態**頁面在 Configuration Manager 中。 如果您也正在規劃變更的權限，您可以這麼做之前重新啟動的應用裝置。  
  
![DWConfig 應用裝置時間](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>另請參閱  
[啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
