---
title: SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
caps.latest.revision: 19
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: fc3dfeafab01480fde7eb195363f46946de30ddd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131634"
---
# <a name="setwindowsserviceidentity-method-wmi-msreportserverconfigurationsetting"></a>SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting)
  讓報表伺服器 Windows 服務以指定之 Windows 使用者的身分執行，並且授與此帳戶足夠的檔案系統權限，以便允許報表伺服器運作。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub SetWindowsServiceIdentity(UseBuiltInAccount as Boolean, _  
    Account as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetWindowsServiceIdentity(boolean UseBuiltInAccount,   
    string Account, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *UseBuiltInAccount*  
 指出指定的帳戶是否為內建 Windows 帳戶。  
  
 *帳戶*  
 要用來執行 Windows 服務的 Windows 帳戶，其格式為 "DOMAIN\alias"。  
  
 *密碼*  
 此帳戶的密碼。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
 當*UseBuiltInAccount*參數設定為`true`和報表伺服器正在 Microsoft[!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)]或 Windows XP 中，值*名稱*，*網域*，和*密碼*參數被忽略，而且是本機系統帳戶。  
  
 當*UseBuiltInAccount*參數設定為`true`和報表伺服器執行 Windows Server 2003，*網域*和*密碼*屬性忽略，而且 [名稱] 欄位必須包含"Builtin\NetworkService"或"Builtin\System"或"Builtin\LocalService"。  
  
 SetWindowsServiceIdentity 方法會在報表伺服器安裝目錄中設定檔案與資料夾的檔案權限。  
  
 中指定的帳戶*帳戶*參數需要`LogonAsService`Windows 中的權限。 此方法會將這個權限授與指定的帳戶。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  