---
title: "SetServiceState 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "SetServiceState (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "SetServiceState 方法"
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 20
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# SetServiceState 方法 (WMI MSReportServer_ConfigurationSetting)
  開啟和關閉報表伺服器 Windows 與 Web 服務。  
  
## 語法  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## 參數  
 *EnableWindowsService*  
 表示 Windows 服務狀態的**布林**值。 值為 **true** 會啟動報表伺服器 Windows 服務。值為 **false** 會停止 Windows 服務。  
  
 *EnableWebService*  
 表示 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 服務狀態的**布林**值。 值為 **true** 會啟動報表伺服器 Web 服務。值為 **false** 會停止 Web 服務。  
  
 *EnableReportManager*  
 表示報表管理員所需狀態的**布林**值。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## 傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## 備註  
  
## 需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 請參閱＜  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  