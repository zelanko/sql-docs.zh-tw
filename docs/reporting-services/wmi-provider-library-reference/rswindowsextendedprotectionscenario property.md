---
title: "RSWindowsExtendedProtectionScenario 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
caps.latest.revision: 6
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# RSWindowsExtendedProtectionScenario 屬性 (WMI MSReportServer_ConfigurationSetting)
  傳回字串值，表示報表伺服器設定為允許的擴充保護案例。  
  
## 語法  
  
```vb  
Public Dim RSWindowsExtendedProtectionScenario As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionScenario;  
```  
  
## 備註  
 傳回字串值，表示報表伺服器設定為允許的擴充保護案例。 如果 WMI 提供者連接的報表伺服器不支援擴充保護，則會傳回 "" (空字串)。  
  
 下列清單顯示有效值：  
  
 `”Any | Proxy | Direct”`  
  
## 範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## 請參閱＜  
 [RSWindowsExtendedProtectionLevel 屬性 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [SetExtendedProtectionSettings 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setextendedprotectionsettings-method-wmi-msreportserver-configurationsetting.md)   
 [含有 Reporting Services 的驗證擴充保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  