---
title: "SetServiceState 方法 (WMI MSReportServer_ConfigurationSetting) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8964b2b0886ffd0483e48c8e9baf91ab9b2dae3d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---setservicestate"></a>SetServiceState ConfigurationSetting 方法
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
 > 從 SQL Server 2016 Reporting Services 累計更新 2 開始，已被取代這項設定。 Web 入口網站將會永遠啟用。 會忽略的值。
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>請參閱＜  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

