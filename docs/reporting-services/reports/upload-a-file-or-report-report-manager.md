---
title: "上傳檔案或報表 (報表管理員) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: "42"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c5934844dd9570ab95ab5641d66a465f57725e55
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="upload-a-file-or-report-report-manager"></a>上傳檔案或報表 (報表管理員)
  報表管理員會提供一項上傳功能，讓您可以將報表、模型和其他檔案加入至報表伺服器，而不需要從用戶端應用程式發行這些項目。 您從檔案系統上傳的檔案會當做項目儲存在報表伺服器上。 您所上傳的檔案類型會決定其儲存方式：  
  
-   .rdl 檔案會儲存成報表。  
  
-   .smdl 檔案會儲存成報表模型。  
  
-   所有其他檔案 (包括共用資料來源 (.rds) 檔案) 則會當做資源上傳。 雖然報表伺服器不會處理資源，但是如果報表伺服器支援檔案的 MIME 類型，您就可以在報表管理員中檢視資源。  
  
### <a name="to-upload-a-file-or-report"></a>若要上傳檔案或報表  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  在報表管理員中，導覽至 **[內容]** 頁面。 導覽至您要加入項目的資料夾。  
  
3.  按一下 [上傳檔案]。  
  
4.  按一下 [瀏覽] 選取要上傳的檔案。 您可以上傳報表定義檔案、影像、文件，或要在報表伺服器上提供使用的任何檔案。  
  
5.  輸入新項目的名稱。 項目名稱可以包含空格，但是不能包含保留字元：; ? : @ & = + , $ / * < > |.  
  
6.  如果您要以新項目取代現有的項目，請選取 [如果項目存在則覆寫]。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [內容頁面 &#40;報表管理員&#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [上傳檔案頁面 &#40;報表管理員&#41;](http://msdn.microsoft.com/library/7bb3166f-9374-4449-b66a-ffb77298507d)   
 [上傳檔案到資料夾](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
