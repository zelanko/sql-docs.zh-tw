---
title: "RSWindowsExtendedProtectionScenario 屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6449b0b9d9e27c860d3246b4992cac6405af731f
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="rswindowsextendedprotectionscenario-property"></a>RSWindowsExtendedProtectionScenario 屬性
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
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>請參閱＜  
 [RSWindowsExtendedProtectionLevel 屬性 &#40;WMI msreportserver_configurationsetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [SetExtendedProtectionSettings 方法 &#40;WMI msreportserver_configurationsetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)   
 [Reporting services 的驗證擴充的保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RsReportServer.config 設定檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
