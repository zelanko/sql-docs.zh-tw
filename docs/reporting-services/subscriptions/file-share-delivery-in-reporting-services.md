---
title: "檔案共用傳遞 Reporting Services 中的 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
ms.assetid: 9f338dd3-f68a-4355-b9d7-9b25dacf3b5e
caps.latest.revision: 54
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5e33585c625c49967304ca36ad91ccc1ebac32f1
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="file-share-delivery-in-reporting-services"></a>Reporting Services 中的檔案共用傳遞
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包括檔案共用傳遞延伸模組，讓您可以傳遞報表到資料夾。 依預設，可以使用檔案共用傳遞延伸模組，且不需額外的組態。 若要順利完成檔案傳遞，您必須設定共用資料夾的寫入權限。 需要寫入者權限的帳戶可以排除訂閱中所設定的認證或針對報表伺服器所設定的「檔案共用帳戶」。 如需檔案共用帳戶的詳細資訊，請參閱[訂閱設定與檔案共用帳戶 &#40;組態管理員&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)。 此外，需要存取報表的使用者必須擁有共用資料夾的讀取權限。  
  
 若要散發報表到檔案共用，您必須定義標準訂閱或資料驅動訂閱。 若要了解如何在資料驅動訂閱中使用檔案共用傳遞，請參閱[建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)。 此外，執行遠端檔案共用訂閱的帳戶需要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 電腦上進行本機登入的權限。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式|  
  
 **本主題內容：**  
  
-   [傳遞給共用資料夾之報表的特性](#bkmk_Characteristics)  
  
-   [目標資料夾](#bkmk_target_folders)  
  
-   [檔案格式](#bkmk_file_formats)  
  
-   [檔案選項](#bkmk_file_options)  
  
##  <a name="bkmk_Characteristics"></a> 傳遞給共用資料夾之報表的特性  
  
-   傳遞給共用資料夾的報表屬於靜態檔案，這和報表伺服器所主控及管理的報表不同。  
  
-   為報表定義的互動式功能 **不適用於** 以檔案形式儲存在檔案系統中的報表。 互動式功能是以靜態元素來表示。 例如，如果您傳遞矩陣報表，所產生的檔案會顯示報表的最上層檢視；您無法展開資料列和資料行來檢視支援的資料。  
  
-   如果報表包括圖表，則使用預設呈現方式。 如果報表連結到其他報表，則連結會轉譯成靜態文字。  
  
-   如果您想要在傳遞的報表中保留互動式功能，請改用電子郵件傳遞。 電子郵件會包含報表伺服器上報表的連結，而且使用者可以使用互動式功能。 如需詳細資訊，請參閱 [Reporting Services 中的電子郵件傳遞](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)。  
  
##  <a name="bkmk_target_folders"></a> 目標資料夾  
 定義使用檔案共用傳遞的訂閱時，必須指定現有的資料夾做為目標資料夾。 報表伺服器不會在檔案系統中建立資料夾。 您指定的資料夾必須可以透過網路連接來存取。  
  
 確認要 **檢視** 共用資料夾中報表的使用者擁有讀取權限。  
  
 在訂閱中指定目標資料夾時，請使用包含電腦網路名稱的統一命名慣例 (UNC) 格式。 資料夾路徑中不要包含尾端的反斜線。 下列範例說明 UNC 路徑：  
  
```  
\\<servername>\reportarchive\operations\2014  
```  
  
 建立資料夾時，請考慮您需要的連接限制。 雖然報表伺服器只需要兩個連接，但您必須包含足夠的連接來滿足其他想要開啟共用資料夾報表的使用者。  
  
##  <a name="bkmk_file_formats"></a> 檔案格式  
 可以使用各種檔案格式 (例如 HTML、DOCX 和 Excel) 來轉譯報表。 若要以特定的檔案格式儲存報表，請在建立您的訂閱時選取該轉譯格式。 例如，選擇 **[Excel]** 會將報表儲存為 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 檔案。 雖然您可以選擇任何支援的轉譯格式，當轉譯檔案時有些格式會運作的比較好。  
  
 若為檔案共用傳遞，請選擇以單一檔案傳遞報表的格式，其中所有影像和相關內容會包括在報表內。 適當的格式包括網頁封存、PDF、TIFF 和 Excel。 請避免使用 HTML4.0。 如果您的報表包含影像，HTML 4.0 格式就不會在檔案中包含這些影像。  
  
##  <a name="bkmk_file_options"></a> 檔案選項  
 當您建立檔案共用訂閱時，可以設定檔案名稱的建立方式，以及檔案是否會覆寫報表的舊版本。 完整檔案名稱有三個部分：名稱、副檔名，以及附加至檔案以建立唯一檔案名稱的文字或數字  
  
 **檔案名稱** ：預設檔案名稱是以來源報表名稱為基礎，但是您可以在訂閱中提供自訂名稱。 副檔名為選擇性，但是如果您有指定副檔名，報表伺服器將會建立對應到轉譯格式的副檔名。  
  
 **覆寫** ：您可以指定覆寫選項，針對每一次報表傳遞重複使用相同的檔案名稱，或者建立新的檔案。 若要覆寫檔案，您必須使用相同的檔案名稱和副檔名。  
  
 有一個替代方式可以在每一次傳遞中建立唯一的檔案，就是在檔案名稱中加入時間戳記。 若要這樣做，請將 **@timestamp** 變數加入檔案名稱 (例如 *CompanySales@timestamp*)。 使用這個方法時，會讓檔案名稱依照定義成為唯一的檔案名稱，所以絕對不會遭到覆寫。  
  
 下圖是針對檔案共用傳遞所設定之訂閱的檔案設定範例。  
  
 ![檔案共用訂閱](../../reporting-services/subscriptions/media/ssrs-file-share-subscription.png "檔案共用訂閱")  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理原生模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [訂閱設定與檔案共用帳戶 &#40;組態管理員&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)  
  
  
