---
title: "使用 URL 存取轉譯報表記錄快照集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "URL 存取 [Reporting Services], 報表記錄"
  - "記錄快照集 [Reporting Services]"
  - "記錄資料 [Reporting Services]"
  - "快照集 [Reporting Services], URL 存取"
  - "快照集 [Reporting Services], 轉譯報表記錄"
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 32
---
# 使用 URL 存取轉譯報表記錄快照集
  您可以提供 *rs:Snapshot* 參數並將其值設定為有效的快照集識別碼，來根據報表記錄快照集轉譯報表。 參數值的格式是 YYYY-MM-DDTHH:MM:SS，此格式符合國際標準組織 (ISO) 8601 標準。  
  
 如果您省略此參數，就會根據報表伺服器的報表執行與快取管理選項設定來轉譯報表。 如需報表執行的詳細資訊，請參閱[設定報表處理屬性](../reporting-services/report-server/set-report-processing-properties.md)。  
  
## 範例  
 下列範例會顯示擷取報表記錄快照集的 URL：  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## 請參閱＜  
 [URL 存取 &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL 存取參數參考](../reporting-services/url-access-parameter-reference.md)  
  
  