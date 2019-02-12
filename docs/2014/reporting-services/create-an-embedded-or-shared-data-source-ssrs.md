---
title: 建立內嵌或共用資料來源 (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], creating
ms.assetid: b111a8d0-a60d-4c8b-b00a-51644b19c34b
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: d9da0718a6eee5fda00d6418a5b6a624f8380c7d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033479"
---
# <a name="create-an-embedded-or-shared-data-source-ssrs"></a>建立內嵌或共用資料來源 (SSRS)
  報表資料來源會指定名稱及連接資訊。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 可支援兩種類型的資料來源：內嵌和共用。 內嵌資料來源是定義在報表定義中，而且只能供該報表使用。 共用資料來源會定義成個別的項目，而且可以供多個報表使用。 如需詳細資訊，請參閱 <<c0> [ 內嵌和共用資料連接或資料來源&#40;報表產生器及 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)。</c0>  
  
 在報表產生器中，您可以瀏覽至報表伺服器或 SharePoint 網站，然後選取資料來源或建立內嵌資料來源。 您無法在報表產生器中建立共用資料來源。  
  
 在報表設計師中，您可以建立共用或內嵌資料來源。 從 [報表資料] 窗格中，開始建立資料來源參考，然後按**新增**選項。 建立資料來源參考之後，新的共用資料來源就會自動加入至 [方案總管] 的 [共用資料來源] 資料夾底下。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 您也可以直接在報表伺服器或 SharePoint 網站上建立共用資料來源。 如需詳細資訊，請參閱 <<c0> [ 建立、 刪除或修改共用資料來源&#40;報表管理員&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)或是[建立和管理共用資料來源&#40;&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).</c0>  
  
### <a name="to-create-an-embedded-or-shared-data-source"></a>建立內嵌或共用資料來源  
  
1.  在 [報表資料] 窗格的工具列上，按一下 **[新增]** ，然後按一下 **[資料來源]**。 **[資料來源屬性]** 對話方塊隨即開啟。  
  
    > [!NOTE]  
    >  如果看不到 [報表資料] 窗格，請按一下 [檢視] 功能表上的 [報表資料]。  
  
2.  在 **[名稱]** 文字方塊中，輸入資料來源的名稱或接受預設值。 資料來源名稱是在報表內部使用。 為了清楚起見，我們建議資料來源的名稱要包含連接字串中所指定的資料庫名稱。  
  
3.  內嵌的資料來源，請確認**內嵌連接**已選取。  
  
    1.  從 [類型] 下拉式清單中，選取資料來源類型，例如 [Microsoft SQL Server] 或 [OLE DB]。  
  
    2.  使用以下其中一個替代方式指定連接字串：  
  
    -   在 **[連接字串]** 文字方塊中直接輸入連接字串。 如需連接字串範例，請參閱[資料連接、 資料來源和報表產生器中的連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)或[資料 Connections，Data Sources，and Connection Strings in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
    -   按一下運算式 (**fx)** 按鈕，即可建立一個評估為連接字串的運算式。 在 **[運算式]** 對話方塊的 [運算式] 窗格內，輸入運算式。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    -   按一下 **[編輯]** ，針對您在步驟 2 中選擇的資料來源類型開啟 **[連接屬性]** 對話方塊。  
  
         依照此資料來源類型適合的情況，填入 **[連接屬性]** 對話方塊中的欄位。 連接屬性包括資料來源的類型、資料來源的名稱以及要使用的認證。 當您在此對話方塊中指定值之後，請按一下 **[測試連接]** 來確認此資料來源確實可用，而且您指定的認證正確無誤。 如需特定資料來源類型的詳細資訊，請參閱[從外部資料來源新增資料 &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md)。  
  
4.  共用的資料來源，請確認**使用共用資料來源參考**已選取。  
  
    1.  按一下 **[新增]**。 在 [共用資料來源] 屬性對話方塊中，遵循步驟 2 和 3 來建立新的資料來源。  
  
    2.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
         新的共用資料來源會出現在 [方案總管] 的 [共用資料來源] 資料夾中。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     資料來源會出現在 [報表資料] 窗格中。 在 [報表資料] 窗格中，共用資料來源會指向資料來源定義。 在報表產生器中，資料來源定義位於報表伺服器或 SharePoint 網站上。 在報表設計師中，資料來源定義是 [方案總管] 中 [共用資料來源] 資料夾底下的檔案。  
  
### <a name="to-import-an-existing-data-source-in-report-designer"></a>若要在報表設計師中匯入現有的資料來源  
  
1.  在方案總管中，以滑鼠右鍵按一下報表伺服器專案中的 [共用資料來源] 資料夾，然後按一下 [加入現有項目]。 [新增現有項目] 對話方塊隨即開啟。  
  
2.  巡覽至現有的報表定義共用資料來源 (rds) 檔案，然後按一下 [開啟]。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-convert-an-embedded-data-source-to-a-shared-data-source-in-report-designer"></a>若要在報表設計師中，將內嵌資料來源轉換成共用資料來源  
  
-   在 報表資料 窗格中，以滑鼠右鍵按一下 資料來源，然後按一下**轉換為共用資料來源**。  
  
### <a name="to-convert-a-shared-data-source-to-an-embedded-data-source-in-report-builder"></a>若要在報表產生器中，將共用資料來源轉換成內嵌資料來源  
  
-   在 報表資料 窗格中，以滑鼠右鍵按一下 資料來源，然後開啟**資料來源屬性**。  
  
-   按一下 **內嵌的連接**並完成先前的程序中所述，建立內嵌的資料來源。  
  
## <a name="see-also"></a>另請參閱  
 [在 Reporting Services 資料來源中儲存認證](report-data/store-credentials-in-a-reporting-services-data-source.md)   
 [內嵌和共用資料連接或資料來源 &#40;報表產生器及 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [共用資料來源，從將內嵌的轉換成&#40;報表產生器及 SSRS&#41;](report-data/convert-data-sources-report-builder-and-ssrs.md)   
 [將報表或模型繫結至共用資料來源 &#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [設定報表的資料來源屬性 &#40;報表管理員&#41;](report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
