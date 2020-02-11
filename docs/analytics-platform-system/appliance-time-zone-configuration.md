---
title: 設定時區
description: '[時區] 頁面可讓您設定分析平臺系統（AP）設備上所有節點的時區。'
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1da16790d011a628bc2536de051eb1181f06b8cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401388"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>設備時區設定-Analytics Platform System
[**時區**] 頁面可讓您設定分析平臺系統（ap）設備上所有節點的時區。  
  
## <a name="to-set-the-time-zone"></a>若要設定時區  
  
1.  啟動 Configuration Manager。 如需詳細資訊，請參閱[&#40;分析平臺系統&#41;啟動 Configuration Manager ](launch-the-configuration-manager.md)。  
  
2.  使用 Configuration Manager 中的 [**服務狀態**] 頁面來停止設備服務。 如需相關指示，請參閱[PDW 服務狀態 &#40;Analytics 平臺系統&#41;](pdw-services-status.md) 。  
  
3.  在 Configuration Manager 的左窗格中，按一下 [**時區**]。 從 [**時區**] 下拉式功能表中選取想要的時區。 視您的位置而定，您也可以選擇選取 [**自動調整日光節約時間的時鐘**] 旁的方塊。  
  
4.  按一下 **[** 套用] 以儲存變更。  
  
5.  使用 Configuration Manager 中的 [**服務狀態**] 頁面重新開機設備服務。 如果您也打算變更許可權，可以在重新開機設備之前執行該動作。  
  
![DWConfig 應用裝置時間](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>另請參閱  
[啟動 Configuration Manager &#40;分析平臺系統&#41;](launch-the-configuration-manager.md)  
  
