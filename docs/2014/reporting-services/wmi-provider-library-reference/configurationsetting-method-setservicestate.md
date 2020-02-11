---
title: SetServiceState 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 21c8de3e6903a28ad8358431f5e455df31d3044e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097945"
---
# <a name="setservicestate-method-wmi-msreportserver_configurationsetting"></a>SetServiceState 方法 (WMI MSReportServer_ConfigurationSetting)
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
 表示 Windows 服務狀態的 `Boolean` 值。 值為 `true` 會啟動報表伺服器 Windows 服務。值為 `false` 會停止 Windows 服務。  
  
 *EnableWebService*  
 表示`Boolean` [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 服務狀態的值。 值為 `true` 會啟動報表伺服器 Web 服務。值為 `false` 會停止 Web 服務。  
  
 *EnableReportManager*  
 表示報表管理員所需狀態的 `Boolean` 值。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="requirements"></a>需求  
 **命名空間：**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
