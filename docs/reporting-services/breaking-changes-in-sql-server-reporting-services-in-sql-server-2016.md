---
title: "SQL Server 2016 中 SQL Server Reporting Services 的重大變更 | Microsoft Docs"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Me.Value 參考"
  - "Reporting Services，回溯相容性"
  - "重大變更 [Reporting Services]"
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 116
---
# SQL Server 2016 中 SQL Server Reporting Services 的重大變更
  本主題描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的重大變更。 這些變更可能會中斷以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 為根據的應用程式、指令碼或功能。 當您進行升級或是在自訂指令碼或報表內時，可能會遇到這些問題。  
  
  ## 安全性延伸模組
  
  自訂安全性延伸模組需要做一些修改，才能使用新的 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]。 安全性延伸模組必須使用 IAuthenticationExtension2 介面。
  
  ## WMI 提供者
  
  [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 應用程式名稱從 "ReportManager" 變更為 "ReportServerWebApp"。
  
## 另請參閱  
 [SQL Server 2016 中 SQL Server Reporting Services 的行為變更](http://msdn.microsoft.com/zh-tw/2a767f0f-84f2-4099-8784-1e37790f858e)   
 [Reporting Services &#40;SSRS&#41; 的新功能](../Topic/What's%20New%20in%20Reporting%20Services%20\(SSRS\).md)   
 [SQL Server 2016 中 SQL Server Reporting Services 已被取代的功能](http://msdn.microsoft.com/zh-tw/3876c01e-f81d-4cce-9104-5106a8c369e6)   
 [SQL Server 2016 中 SQL Server Reporting Services 已停止的功能](http://msdn.microsoft.com/zh-tw/d529cc96-3483-480b-9bfc-bd28b1d0ef52)  
  
  