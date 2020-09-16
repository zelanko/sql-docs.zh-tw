---
description: ReencryptSecureInformation 方法 (WMI MSReportServer_ConfigurationSetting)
title: ReencryptSecureInformation 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 629df7fb638bbad4df760855ae7963dce763071b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468968"
---
# <a name="configurationsetting-method---reencryptsecureinformation"></a>ConfigurationSetting 方法 - ReencryptSecureInformation
  產生新的加密金鑰，並且使用這個新的金鑰來重新加密目錄中的所有安全資訊。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub ReencryptSecureInformation(ByRef HRESULT as Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ReencryptSecureInformation (out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>參數  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
 *ExtendedErrors[]*  
 [out] 包含呼叫所傳回之其他錯誤的字串陣列。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
 ReencryptSecureInformation 方法可讓管理員將現有的加密金鑰取代成新的金鑰。  
  
 叫用這個方法時，報表伺服器就會產生新的加密金鑰，並且逐一查看所有加密的內容，以便使用新的加密金鑰來重新加密內容。  
  
 傳遞延伸模組可以將安全資訊儲存在其傳遞設定結構中。 呼叫 ReencryptSecureInformation 時，報表伺服器就會載入每個訂閱和對應的傳遞延伸模組，以便重新加密儲存在相關聯設定中的資訊。  
  
 如果這個方法是在向外延展部署中的電腦上執行，則向外延展部署中的每部電腦都必須再次初始化。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
