---
title: SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d08e9900453fe259d727e202489d728e0dce47e0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097881"
---
# <a name="setwindowsserviceidentity-method-wmi-msreportserver_configurationsetting"></a>SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting)
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
 當*UseBuiltInAccount*參數設定為`true` ，而且報表伺服器正在 Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)]或 Windows XP 上執行時，會忽略*Name*、 *Domain*和*Password*參數的值，並使用本機系統帳戶。  
  
 當*UseBuiltInAccount*參數設定為`true` ，而且報表伺服器在 Windows server 2003 上執行時，會忽略*網域*和*密碼*屬性，而且 [名稱] 欄位必須包含 "Builtin\NetworkService" 或 "Builtin\System" 或 "Builtin\LocalService"。  
  
 SetWindowsServiceIdentity 方法會在報表伺服器安裝目錄中設定檔案與資料夾的檔案權限。  
  
 *帳戶*參數中指定的帳號需要`LogonAsService` Windows 中的許可權。 此方法會將這個權限授與指定的帳戶。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
