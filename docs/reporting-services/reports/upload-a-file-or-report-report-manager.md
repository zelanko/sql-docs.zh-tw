---
title: 在報表伺服器中上傳檔案或報表 | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ce224e5b45e22bdc27f675da5d2697c09b139b41
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47660196"
---
# <a name="upload-a-file-or-report-in-the-report-server"></a>在報表伺服器中上傳檔案或報表
報表伺服器的 Web 入口網站會提供一項上傳功能，讓您可以將報表和其他檔案新增至報表伺服器，而不需要從用戶端應用程式發行這些項目。 您從檔案系統上傳的檔案會當做項目儲存在報表伺服器上。 您所上傳的檔案類型會決定其儲存方式：  
  
-   .rdl 檔案會儲存成分頁報表。  
  
-   所有其他檔案 (包括共用資料來源 (.rds) 檔案) 則會當做資源上傳。 雖然報表伺服器不會處理資源，但是如果報表伺服器支援檔案的 MIME 類型，您就可以在 Web 入口網站中檢視資源。  
  
### <a name="to-upload-a-file-or-report"></a>若要上傳檔案或報表  
  
1.  在 Web 入口網站中，按一下 [上傳]。  
  
4.  瀏覽至您想要上傳的檔案。 您可以上傳報表定義檔案、影像、文件，或要在報表伺服器上提供使用的任何檔案。  
  
5.  輸入新項目的名稱。 項目名稱可以包含空格，但是不能包含保留字元：\; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|。  
  
6.  如果您要以新項目取代現有的項目，請選取 [如果項目存在則覆寫]。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱   
[建立、修改及刪除共用資料來源](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)
[上傳檔案至資料夾](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
