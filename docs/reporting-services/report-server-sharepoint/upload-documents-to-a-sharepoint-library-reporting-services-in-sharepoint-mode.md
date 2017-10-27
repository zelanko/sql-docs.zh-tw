---
title: "將文件上傳至 SharePoint 文件庫 (SharePoint 模式的 Reporting Services) |Microsoft 文件"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: d938f068ecf2d0c2a2b920fda9f7c414649f069d
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode"></a>將文件上傳至 SharePoint 文件庫 (SharePoint 模式的 Reporting Services)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

您可以將報表定義和報表模型上傳到 SharePoint 文件庫。 上傳報表伺服器項目時，您必須選取文件庫或文件庫內的資料夾； 不能將報表伺服器項目上傳到清單或頁面中。  

> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

 您無法上傳資料來源 (.rds) 檔案。 不過，您可以從設計工具 (例如，報表設計師) 將 .rds 檔案發行到 SharePoint 文件庫。 在發行過程中，方案會從原始的 .rsds 檔案建立新的 .rds 檔案。 您也可以在 SharePoint 文件庫中建立新的 .rsds 檔案，然後再設定已上傳的報表和模型中的資料來源連接屬性，以使用新的連接。  
  
> [!NOTE]  
>  報表伺服器必須設定為 SharePoint 模式和 SharePoint 產品的執行個體必須在 Reporting Services 增益集，提供儲存和存取報表伺服器項目從 SharePoint 網站的程式檔案。  
  
 若要將文件上傳至文件庫，您必須擁有網站層級的「加入項目」權限。 如果您使用預設安全性設定，此權限授與成員的**擁有者**群組具有完整控制權限等級的權限和**成員**擁有 「 參與 」 等級權限的群組。  
  
## <a name="add-a-report-definition-or-report-model-to-a-library"></a>將報表定義或報表模型加入至文件庫
  
1.  開啟文件庫或文件庫內的資料夾。 如果尚未開啟文件庫，請按一下 [快速啟動] 上的文件庫名稱。 如果找不到您的文件庫名稱，請先按一下 **[檢視所有網站內容]**，然後再按一下文件庫名稱。  
  
2.  在**上傳**功能表上，按一下 **上傳文件**。  
  
3.  若要上傳的單一報表或報表模型檔案，選取報表定義 (.rdl) 或報表模型 (.smdl) 檔案，然後按一下**確定**。  
  
     如果報表定義使用共用資料來源 (.rsds) 檔案，將連接資訊儲存在外部資料來源中，您可以同時上傳 .rdl 和 .rsds 檔案。 若要這樣做，請按一下**上傳多份文件**，指定兩個檔案，然後按**確定**。  
  
 如果您上傳的報表包含共用資料來源、報表模型或子報表的參考，上傳檔案時，報表中的參考將會中斷。 如需如何重設參考的詳細資訊，請參閱[建立和管理共用資料來源 &#40;Reporting Services SharePoint 整合模式 &#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 上傳報表後，報表會在您開啟時視需要執行，以擷取資料來源中的即時資料。 您可以設定讓報表依排程擷取資料或使用快取資料。 如需詳細資訊，請參閱[設定處理選項 &#40;Reporting Services SharePoint 整合模式 &#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
 報表可以包含參數，以便讓使用者篩選資料。 您可將參數設定成使用特定值，或變更使用者看到的參數外觀。 如需詳細資訊，請參閱[已發行的報表 &#40; 上的 設定參數Reporting Services SharePoint 整合模式 &#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>另請參閱

 [將報表發行到 SharePoint 文件庫](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [將共用的資料來源發行至 SharePoint 文件庫](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

