---
title: SetServiceState 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7e17d962dce18a3d5f384ba07ff37a1d1f67b7f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configurationsetting-method---setservicestate"></a>ConfigurationSetting 方法 - SetServiceState
  開啟和關閉報表伺服器 Windows 與 Web 服務。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetServiceState(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *EnableWindowsService*  
 表示 Windows 服務狀態的 **布林** 值。 值為 **true** 會啟動報表伺服器 Windows 服務。值為 **false** 會停止 Windows 服務。  
  
 *EnableWebService*  
 表示 **Web 服務狀態的** 布林 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 值。 值為 **true** 會啟動報表伺服器 Web 服務。值為 **false** 會停止 Web 服務。  
  
 *EnableReportManager*  
 表示報表管理員所需狀態的 **布林** 值。
 
 > [!NOTE] 
 > 此設定已在 SQL Server 2016 Reporting Services 累積更新 2 之後淘汰。 入口網站會一律啟用。 將會忽略值。
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
