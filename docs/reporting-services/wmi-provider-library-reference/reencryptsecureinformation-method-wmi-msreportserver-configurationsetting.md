---
title: "ReencryptSecureInformation 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
apiname: 
  - "ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "ReencryptSecureInformation 方法"
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# ReencryptSecureInformation 方法 (WMI MSReportServer_ConfigurationSetting)
  產生新的加密金鑰，並且使用這個新的金鑰來重新加密目錄中的所有安全資訊。  
  
## 語法  
  
```vb  
Public Sub ReencryptSecureInformation(ByRef HRESULT as Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ReencryptSecureInformation (out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## 參數  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
 *ExtendedErrors[]*  
 [out] 包含呼叫所傳回之其他錯誤的字串陣列。  
  
## 傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## 備註  
 ReencryptSecureInformation 方法可讓管理員將現有的加密金鑰取代成新的金鑰。  
  
 叫用這個方法時，報表伺服器就會產生新的加密金鑰，並且逐一查看所有加密的內容，以便使用新的加密金鑰來重新加密內容。  
  
 傳遞延伸模組可以將安全資訊儲存在其傳遞設定結構中。 呼叫 ReencryptSecureInformation 時，報表伺服器就會載入每個訂閱和對應的傳遞延伸模組，以便重新加密儲存在相關聯設定中的資訊。  
  
 如果這個方法是在向外延展部署中的電腦上執行，則向外延展部署中的每部電腦都必須再次初始化。  
  
## 需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 請參閱＜  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  