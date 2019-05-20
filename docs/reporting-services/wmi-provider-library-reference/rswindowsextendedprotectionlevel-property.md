---
title: RSWindowsExtendedProtectionLevel 屬性 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7854821a9f43bc234490d915ff75339e250f6c39
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571073"
---
# <a name="rswindowsextendedprotectionlevel-property"></a>RSWindowsExtendedProtectionLevel 屬性
  傳回字串值，表示報表伺服器設定為支援的保護等級。 此屬性是唯讀的。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>Remarks  
 傳回字串值，表示報表伺服器設定為支援的保護等級。 如果 WMI 提供者連線的報表伺服器不支援擴充保護，則會傳回 "" (空字串)。 下列清單顯示有效值：  
  
 `"Off" | "Allow" | "Require"`  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>另請參閱  
 [RSWindowsExtendedProtectionScenario 屬性 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [SetExtendedProtectionSettings 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)   
 [Reporting Services 的驗證擴充保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
