---
title: RSWindowsExtendedProtectionScenario 屬性 (WMI MSReportServer_ConfigurationSetting) |Microsoft 文件
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: f6fa7fa258d4638f6dbe7d6626e067b95882a779
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030942"
---
# <a name="rswindowsextendedprotectionscenario-property-wmi-msreportserverconfigurationsetting"></a>RSWindowsExtendedProtectionScenario 屬性 (WMI MSReportServer_ConfigurationSetting)
  傳回字串值，表示報表伺服器設定為允許的擴充保護案例。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Dim RSWindowsExtendedProtectionScenario As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionScenario;  
```  
  
## <a name="remarks"></a>備註  
 傳回字串值，表示報表伺服器設定為允許的擴充保護案例。 如果 WMI 提供者連接的報表伺服器不支援擴充保護，則會傳回 "" (空字串)。  
  
 下列清單顯示有效值：  
  
 `”Any | Proxy | Direct”`  
  
## <a name="example-code"></a>範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>另請參閱  
 [RSWindowsExtendedProtectionLevel 屬性&#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionlevel-property.md)   
 [SetExtendedProtectionSettings 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setextendedprotectionsettings.md)   
 [Reporting Services 的驗證擴充保護](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [RSReportServer 組態檔](../report-server/rsreportserver-config-configuration-file.md)  
  
  