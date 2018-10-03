---
title: SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 81b0ea8c7142f33ef9fc91622d899e54f21fe756
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076210"
---
# <a name="setextendedprotectionsettings-method-wmi-msreportserverconfigurationsetting"></a>SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting)
  使用 SetExtendedProtectionSettings 方法可在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態檔 RSReportServer.config 中設定 RSWindowsExtendedProtectionLevel 和 RSWindowsExtendedProtectionScenario 屬性。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub SetExtendedProtectionSettings( _  
        ByVal ExtendedProtectionLevel As String, _  
        ByVal ExtendedProtectionScenario As String, _  
        ByRef Warnings() As String, _  
        ByRef Length As Int32, _  
        ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetExtendedProtectionSettings(  
            string ExtendedProtectionLevel,  
            string ExtendedProtectionScenario,  
            out string[] Warnings,  
            out Int32 Length,  
            out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *ExtendedProtectionLevel*  
 在 RSRreportserver.config 檔案中設定 RSWindowsExtendedProtectionLevel。 所需的值不區分大小寫。  
  
 下列清單顯示有效值：  
  
 `”Off | Allow | Require”`  
  
 *ExtendedProtectionScenario*  
 在 RSReportserver.config 檔案中設定 RSWindowsExtendedProtectionScenario。 所需的值不區分大小寫。  
  
 下列清單顯示有效值：  
  
 `”Any” | “Proxy” | “Direct”`  
  
## <a name="remarks"></a>備註  
 當 RSReportServer.config 檔案中的 AuthenticationTypes 包括 RSWindowNTLM、RSWindowsNegotiate 或 RSWindowsKerberos 時，便會套用 RSWindowsExtendedProtectionLevel 和 the RSWindowsExtendedProtectionScenario 屬性。 設定這些屬性會影響使用者和用戶端軟體向報表伺服器驗證的方式。 建議您閱讀擴充保護，再將 ExtendedProtectionLevel 設定為其中一個的文件`Allow`或`Require`。  
  
 若要設定 ExtendedProtectionLevel，使用者必須是報表伺服器上 BUILTIN\Administrators 群組的成員。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [RSWindowsExtendedProtectionScenario 屬性&#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionscenario-property.md)   
 [RSWindowsExtendedProtectionLevel 屬性&#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionlevel-property.md)   
 [Reporting Services 的驗證擴充保護](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [RSReportServer 設定檔](../report-server/rsreportserver-config-configuration-file.md)  
  
  
