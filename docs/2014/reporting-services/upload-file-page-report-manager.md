---
title: 上傳檔案頁面 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7bb3166f-9374-4449-b66a-ffb77298507d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1100baa3cd72a04d208b2076d91ca4efed7d38e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098871"
---
# <a name="upload-file-page-report-manager"></a>上傳檔案頁面 (報表管理員)
  您可以使用 [上傳檔案] 頁面，將檔案從檔案系統發行至報表伺服器資料庫。 在報表伺服器資料夾階層中，上傳的檔案會以項目來表示。  
  
-   上傳的 .rdl 檔案會以報表發行至報表伺服器。  
  
-   如果上傳的 .smdl 檔案包含資料來源檢視資訊，則會將其當做報表模型來發行。 如果遺漏資料來源檢視參考，在上傳期間便會發生錯誤。 如果您從 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 報表模型專案上傳 .smdl 檔案，就有可能會遺漏資料來源檢視資訊。 在報表模型專案中，資料來源檢視資訊是儲存在個別的檔案中，而不是儲存在 .smdl 檔案中。  
  
     包含資料來源檢視資訊 (因此可成功上傳) 的模型檔案是先前發行到報表伺服器，之後從伺服器儲存到檔案系統的檔案。 如果您開啟模型的 [一般屬性] 頁面，並按一下 **[編輯]** 開啟模型，就可以將模型儲存至檔案，然後將其當做新的模型上傳至報表伺服器。 隨後上傳的 .smdl 檔案將具有模型發行集需要的所有資訊。  
  
-   您上傳的所有其他檔案類型都會儲存成資源。 這包括含有報表資料來源連接資訊的 .rds 檔案。 上傳 .rds 檔案並不會在報表伺服器上產生共用資料來源項目。  
  
 上傳項目時，它會放置於目前的資料夾中。 完成上傳之後，您就可以將項目移至不同位置。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-upload-file-page"></a>若要開啟上傳檔案頁面  
  
1.  開啟報表管理員中，然後導覽至您想要在其中上傳檔案的資料夾。  
  
2.  在工具列中，按一下 **[上傳檔案]** 。  
  
## <a name="options"></a>選項  
 **要上傳的檔案**  
 顯示您要從檔案系統複製的完整檔案路徑。  
  
 **瀏覽**  
 按一下即可從檔案系統選擇檔案。  
  
 **名稱**  
 輸入檔案名稱，此名稱將顯示在報表伺服器命名空間中。 名稱必須至少包含一個英數字元。 也可以包含空格和特定符號。 請勿使用 ; ? : \@ & = +，$ * \< > |"或 / 來指定項目名稱。  
  
 **如果它存在於項目覆寫**  
 若要以新版本取代現有的項目，請選取此核取方塊。 若要覆寫現有的版本，新項目的名稱與現有項目的名稱必須完全相符。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [內容頁面 &#40;報表管理員&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [上傳檔案到資料夾](report-server/upload-files-to-a-folder.md)  
  
  
