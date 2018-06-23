---
title: SetServiceState 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 17
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 7fdcc309eca07c8fc29fa80934e6929054a59b44
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132343"
---
# <a name="setservicestate-method-wmi-msreportserverconfigurationsetting"></a>SetServiceState 方法 (WMI MSReportServer_ConfigurationSetting)
  開啟和關閉報表伺服器 Windows 與 Web 服務。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *EnableWindowsService*  
 A`Boolean`值，表示 Windows 服務的狀態。 值為`true`啟動報表伺服器 Windows 服務，而值`false`停止 Windows 服務。  
  
 *EnableWebService*  
 A`Boolean`值，指出狀態的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Web 服務。 值為 `true` 會啟動報表伺服器 Web 服務。值為 `false` 會停止 Web 服務。  
  
 *EnableReportManager*  
 A`Boolean`值，指出報表管理員所需的狀態。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  