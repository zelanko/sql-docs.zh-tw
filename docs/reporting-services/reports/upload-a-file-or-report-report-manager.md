---
title: "上傳檔案或報表 (報表管理員) | Microsoft Docs"
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
  - "發行報表 [Reporting Services], 上傳檔案"
  - "報表 [Reporting Services], 發行"
  - "上傳報表 [Reporting Services]"
  - "上傳檔案 [Reporting Services]"
  - "檔案 [Reporting Services], 上傳"
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# 上傳檔案或報表 (報表管理員)
  報表管理員會提供一項上傳功能，讓您可以將報表、模型和其他檔案加入至報表伺服器，而不需要從用戶端應用程式發行這些項目。 您從檔案系統上傳的檔案會當做項目儲存在報表伺服器上。 您所上傳的檔案類型會決定其儲存方式：  
  
-   .rdl 檔案會儲存成報表。  
  
-   .smdl 檔案會儲存成報表模型。  
  
-   所有其他檔案 (包括共用資料來源 (.rds) 檔案) 則會當做資源上傳。 雖然報表伺服器不會處理資源，但是如果報表伺服器支援檔案的 MIME 類型，您就可以在報表管理員中檢視資源。  
  
### 若要上傳檔案或報表  
  
1.  啟動[報表管理員 &#40;SSRS 原生模式&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)。  
  
2.  在報表管理員中，導覽至 **[內容]** 頁面。 導覽至您要加入項目的資料夾。  
  
3.  按一下 [上傳檔案]。  
  
4.  按一下 [瀏覽] 以選取要上傳的檔案。 您可以上傳報表定義檔案、影像、文件，或要在報表伺服器上提供使用的任何檔案。  
  
5.  輸入新項目的名稱。 項目名稱可以包含空格，但是不能包含保留字元：; ? : @ & = + , $ / * \< > |.  
  
6.  如果您要以新項目取代現有的項目，請選取 [如果項目存在則覆寫]。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 請參閱＜  
 [建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../Topic/Create,%20Delete,%20or%20Modify%20a%20Shared%20Data%20Source%20\(Report%20Manager\).md)   
 [內容頁面 &#40;報表管理員&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [上傳檔案頁面 &#40;報表管理員&#41;](../Topic/Upload%20File%20Page%20\(Report%20Manager\).md)   
 [上傳檔案到資料夾](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  