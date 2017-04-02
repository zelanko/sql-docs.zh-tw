---
title: "DatabaseLogonType 屬性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
apiname: 
  - "DatabaseLogonType"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "DatabaseLogonType 屬性"
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
caps.latest.revision: 24
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# DatabaseLogonType 屬性 (WMI MSReportServer_ConfigurationSetting)
  指定報表伺服器會使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 服務帳戶、Windows 使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入來存取報表伺服器資料庫。 唯讀。  
  
## 語法  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## 屬性值  
 代表登入類型的 **integer** 物件。  
  
## 範例程式碼  
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## 備註  
 值為：  
  
-   0 代表 Windows 登入  
  
-   1 代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入  
  
-   2 代表要當做服務登入  
  
 如果您指定了 0 (Windows)，就必須將 [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/databaselogonaccount-property-wmi-msreportserver-configurationsetting.md) 屬性中的值設定為對應的有效 Windows 使用者帳戶。  
  
 如果您指定 1 (SQL Server)，請確定 [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/databaselogonaccount-property-wmi-msreportserver-configurationsetting.md) 的值對應至有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 如果您指定了 2 (Windows 服務)，報表伺服器就會使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帳戶和 Windows 服務帳戶來存取報表伺服器資料庫。 會忽略 DatabaseLogonAccount 屬性。  
  
## 需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 請參閱＜  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  