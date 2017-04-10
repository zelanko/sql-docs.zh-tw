---
title: "GetReportServerUrls 方法 (WMI MSReportServer_Instance) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "GetReportServerUrls 方法"
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# GetReportServerUrls 方法 (WMI MSReportServer_Instance)
  傳回使用者可用來存取報表伺服器和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]的 URL 清單。  
  
## 語法  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## 參數  
 *ApplicationName[]*  
 包含已安裝之應用程式的陣列。 值為 **ReportServerWebService** 或 **ReportServerWebApp**。  
  
 *URLs[]*  
 包含成功註冊之 URL 的陣列。  
  
 *長度*  
 包含傳回之陣列長度的整數值。  
  
 *HRESULT*  
 表示成功的值或錯誤碼。  
  
## 傳回值  
  
## 備註  
 WMI 管理物件所公開的方法是透過 InvokeMethod 函數呼叫的。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework WMI 文件集中的＜針對管理物件執行方法＞。  
  
## 需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## 請參閱＜  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  