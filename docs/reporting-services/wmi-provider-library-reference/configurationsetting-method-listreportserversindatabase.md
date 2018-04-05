---
title: ListReportServersInDatabase 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c3e8899e2a3fbb77f218a9b3d2108829d3544a2d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---listreportserversindatabase"></a>ConfigurationSetting 方法 - ListReportServersInDatabase
  傳回存在報表伺服器資料庫中之報表伺服器安裝的清單，不論它們是否具有安全資訊的存取權都一樣。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub ListReportServersInDatabase(ByRef MachineNames() As String, _  
    ByRef InstanceNames() As String, ByRef InstallationIDs() As String, _  
    ByRef IsInitialized() As Boolean, ByRef Length As Int32, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] MachineNames,   
    out string[] InstanceNames, out string[] InstallationIDs,   
    out Boolean[] IsInitialized,out Int32 Length, out Int32 HRESULT,    
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>參數  
 *MachineNames[]*  
 [out] 包含資料庫中報表伺服器安裝之電腦名稱的陣列。  
  
 *InstanceNames[]*  
 [out] 包含資料庫中每個報表伺服器安裝之執行個體名稱的陣列。  
  
 *InstallationIDs[]*  
 [out] 包含資料庫中每個報表伺服器安裝之安裝識別碼的陣列。  
  
 *IsInitialized[]*  
 [out] 包含資料庫中每個報表伺服器安裝之初始化狀態的陣列。  
  
 *長度*  
 [out] 此方法所傳回之陣列的長度。 所有傳回的陣列都具有相同的長度。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
 *ExtendedErrors[]*  
 [out] 包含呼叫所傳回之其他錯誤的字串陣列。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>Remarks  
 ListReportServersInDatabase 會列出存在報表伺服器資料庫中的報表伺服器安裝，不論它們是否具有安全資訊的存取權都一樣，並且傳回一組包含每個安裝之資訊的相符陣列。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
