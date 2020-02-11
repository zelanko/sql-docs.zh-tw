---
title: 將檔上傳至 SharePoint 文件庫（SharePoint 模式下的 Reporting Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- SharePoint integration [Reporting Services], content management
- uploading reports [Reporting Services]
ms.assetid: 93bd1b19-061b-409f-8dc2-ec416b2f4b39
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 009d7527f71966003d02e5963de451fda9710ae4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66098843"
---
# <a name="upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode"></a>將文件上傳到 SharePoint 文件庫 (SharePoint 模式的 Reporting Services)
  您可以將報表定義和報表模型上傳到 SharePoint 文件庫。 上傳報表伺服器項目時，您必須選取文件庫或文件庫內的資料夾； 不能將報表伺服器項目上傳到清單或頁面中。  
  
 您無法上傳資料來源 (.rds) 檔案。 不過，您可以從設計工具 (例如，報表設計師) 將 .rds 檔案發行到 SharePoint 文件庫。 在發行過程中，方案會從原始的 .rsds 檔案建立新的 .rds 檔案。 您也可以在 SharePoint 文件庫中建立新的 .rsds 檔案，然後再設定已上傳的報表和模型中的資料來源連接屬性，以使用新的連接。  
  
> [!NOTE]  
>  您必須針對 SharePoint 模式設定報表伺服器，同時 SharePoint 產品的執行個體必須具有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集，以便提供從 SharePoint 網站儲存及存取報表伺服器項目的程式檔案。  
  
 若要將文件上傳至文件庫，您必須擁有網站層級的「加入項目」權限。 如果使用預設安全性設定，擁有完整控制權限等級的**擁有者**群組和擁有「參與」(Contribute) 權限等級的**成員**群組都會取得這個權限。  
  
### <a name="to-add-a-report-definition-or-report-model-to-a-library"></a>將報表定義或報表模型加入至文件庫  
  
1.  開啟文件庫或文件庫內的資料夾。 如果尚未開啟文件庫，請按一下 [快速啟動] 上的文件庫名稱。 如果找不到您的文件庫名稱，請先按一下 **[檢視所有網站內容]** ，然後再按一下文件庫名稱。  
  
2.  在 [上傳]  功能表上，按一下 [上傳文件]  。  
  
3.  若要上傳單一報表或報表模型檔案，請選取報表定義 (.rdl) 或報表模型 (.smdl) 檔案，然後按一下 [確定]****。  
  
     如果報表定義使用共用資料來源 (.rsds) 檔案，將連接資訊儲存在外部資料來源中，您可以同時上傳 .rdl 和 .rsds 檔案。 若要這樣做，請按一下 [上傳多份文件]****，指定要上傳的兩個檔案，然後按一下 [確定]****。  
  
 如果您上傳的報表包含共用資料來源、報表模型或子報表的參考，上傳檔案時，報表中的參考將會中斷。 如需如何重設參考的詳細資訊，請參閱[建立和管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)。  
  
 上傳報表後，報表會在您開啟時視需要執行，以擷取資料來源中的即時資料。 您可以設定讓報表依排程擷取資料或使用快取資料。 如需詳細資訊，請參閱[設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../2014/reporting-services/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)。  
  
 報表可以包含參數，以便讓使用者篩選資料。 您可將參數設定成使用特定值，或變更使用者看到的參數外觀。 如需詳細資訊，請參閱[在已發行的報表上設定參數 &#40;SharePoint 整合模式的 Reporting Services&#41;](report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)。  
  
## <a name="see-also"></a>另請參閱  
 [將報表發行到 SharePoint 文件庫](reports/publish-a-report-to-a-sharepoint-library.md)   
 [將共用資料來源發行至 SharePoint 文件庫](reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
