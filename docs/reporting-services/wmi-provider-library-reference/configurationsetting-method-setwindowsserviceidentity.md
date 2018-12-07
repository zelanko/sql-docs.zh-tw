---
title: SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a63512de9229f26e6e04ad5f44c5dd1c757cb881
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391691"
---
# <a name="configurationsetting-method---setwindowsserviceidentity"></a>ConfigurationSetting 方法 - SetWindowsServiceIdentity
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
  
## <a name="remarks"></a>Remarks  
 當 *UseBuiltInAccount* 參數設定為 **true** ，而且報表伺服器正在 Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] 或 Windows XP 上執行時，系統會忽略 *Name*、 *Domain*和 *Password* 參數的值並且使用本機系統帳戶。  
  
 當 *UseBuiltInAccount* 參數設定為 **true** ，且報表伺服器正在 Windows Server 2003 上執行時，系統會忽略 *Domain* 和 *Password* 屬性，而且名稱欄位必須包含 "Builtin\NetworkService"、"Builtin\System" 或 "Builtin\LocalService"。  
  
 SetWindowsServiceIdentity 方法會在報表伺服器安裝目錄中設定檔案與資料夾的檔案權限。  
  
 *Account* 參數中指定的帳戶需要 Windows 中的 **LogonAsService** 權限。 此方法會將這個權限授與指定的帳戶。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
