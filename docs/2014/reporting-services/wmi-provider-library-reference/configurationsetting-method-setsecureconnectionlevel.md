---
title: SetSecureConnectionLevel 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
caps.latest.revision: 21
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: f761337d48cc168ee87a0557201b5827a80afd21
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032937"
---
# <a name="setsecureconnectionlevel-method-wmi-msreportserverconfigurationsetting"></a>SetSecureConnectionLevel 方法 (WMI MSReportServer_ConfigurationSetting)
  設定報表伺服器的安全連接層級。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub SetSecureConnectionLevel(Level as Integer, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Int32 Level,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *Level*  
 代表安全連接層級的整數值。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
 呼叫時，報表伺服器的 SecureConnectionLevel 屬性會設定為指定的值。 值為 0 時，表示 SSL 為關閉狀態。 值大於或等於 1 時，表示 SSL 為開啟狀態。  
  
-   當設定值時，會變更報表伺服器組態檔中的 SecureConnectionLevel 項目，而`URLRoot`組態檔中的元素設定為使用"https://"（如果指定*層級*大於或如果，等於 1 或"http://"指定*層級*為 0。  
  
 在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]中，SecureConnectionLevel 會變成 on/off 開關，預設值為 0。 對於大於或等於 1，且通過 SetSecureConnectionLevel 方法 API 的任何值，都會將 SSL 視為開啟狀態，並且在 rsreportserver.config 檔案中據此設定組態屬性 SecureConnectionLevel。 基於回溯相容性，仍然允許使用值 2 和 3。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  