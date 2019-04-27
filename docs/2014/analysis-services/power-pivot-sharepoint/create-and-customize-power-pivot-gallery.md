---
title: 建立及自訂 PowerPivot 圖庫 |Microsoft Docs
ms.custom: ''
ms.date: 09/01/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b5cd35e0-3d8f-4784-9172-93d60c730321
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1f753856fbec3fe521cf23e6506c3b43e5dec481
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62749614"
---
# <a name="create-and-customize-powerpivot-gallery"></a>建立及自訂 PowerPivot 圖庫
  PowerPivot 圖庫是一種特殊類型的 SharePoint 文件庫，針對包含 PowerPivot 資料的已發行 Excel 活頁簿和 Reporting Services 報表，提供豐富的預覽與文件管理功能。  
  
##  <a name="bkmk_top"></a> 本主題內容  
  
-   [必要條件](#prereq)  
  
-   [概觀](#overview)  
  
-   [建立 PowerPivot 圖庫](#createlib)  
  
-   [自訂 PowerPivot 圖庫文件庫](#customize)  
  
-   [停用或隱藏重新整理按鈕](#bkmk_hide_refresh_button)  
  
-   [切換至劇場檢視或圖庫檢視](#switch)  
  
##  <a name="prereq"></a> 必要條件  
  
-   您必須有 Silverlight。 您可以透過 Microsoft Update 下載並安裝 Silverlight。 如果您使用沒有 Silverlight 的瀏覽器檢視 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫文件庫，按一下頁面上的連結即可安裝它。 安裝後，您必須先關閉瀏覽器再重新開啟。  
  
    > [!NOTE]  
    >  Power Pivot 圖庫需要 Microsoft Silverlight，  但 Microsoft Edge 瀏覽器不支援 Silverlight。   
    > 若要檢視 Edge 中的程式庫內容，請按一下 Powerpivot 圖庫中的 [程式庫]  索引標籤，然後將文件庫檢視變更為 [所有文件] 。    
    > 若要變更預設檢視，請按一下 [程式庫]  索引標籤，然後按一下 [修改檢視]。 按一下 [設定為預設檢視]，然後按一下 [確定] 以儲存預設檢視。  
    >  如需 Edge 支援的詳細資訊，請參閱 Windows 部落格[揮別以往，第 2 部分：ActiveX、 VBScript...說再見](http://blogs.windows.com/msedgedev/2015/05/06/a-break-from-the-past-part-2-saying-goodbye-to-activex-vbscript-attachevent/)  
  
-   您必須是網站擁有者才能建立文件庫。  
  
-   您必須具備「參與」或更大的權限，才能發行或上傳檔案。  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫不可在受限制的網站中。 包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫的父網站，必須加入信任的網站或近端內部網路區域。  
  
-   必須已為您的應用程式部署 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Web 應用程式方案，且必須已為網站集合啟用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能。 如需詳細資訊，請參閱 <<c0> [ 部署 PowerPivot 方案部署到 SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)並[在管理中心為網站集合啟用 PowerPivot 功能整合](activate-power-pivot-integration-for-site-collections-in-ca.md)。  
  
-   若要檢視或建立以 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿為基礎的 Reporting Services 報表，活頁簿和報表必須在相同的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫中。 報表必須使用包含內嵌資料的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿，不然活頁簿最多只能包含一個是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的外部資料來源。  
  
##  <a name="overview"></a> 概觀  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫是一個文件庫範本，當您在 SharePoint 伺服器上安裝 [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] 時，可以使用該圖庫。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫結合準確的檔案內容預覽與文件來源相關事實。 您可以立即看到文件建立者以及上次修改文件的日期。 若要建立預覽影像， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫會使用可以讀取包含 PowerPivot 資料之 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿與 Reporting Services 報表的快照服務。 如果您發行快照服務無法讀取的檔案，該檔案就沒有預覽影像。  
  
 預覽圖像是以 Excel Services 轉譯活頁簿的方式為基礎。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫中的展示方式應該與您在瀏覽器中檢視 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿時所看到的外觀相同。 不過，預覽的介面區有限。 活頁簿或報表的部分可以修整，以便符合可用空間。 您可能需要開啟活頁簿或報表來檢視完整的文件。  
  
 重新整理來自外部的資料來源的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿資料，在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫中受到完整支援，但需要額外的設定。 伺服器陣列或服務管理員必須將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫新增為 Excel Services 信任位置。 如需相關資訊，請參閱 [在管理中心建立 PowerPivot 網站的信任位置](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
##  <a name="createlib"></a> 建立 PowerPivot 圖庫  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 時，將會為您建立 [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] 圖庫。 如果您將 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 加入至現有的伺服器陣列，或是您想要其他的文件庫，則可以為應用程式或網站建立一個新的文件庫。  
  
1.  1.  **SharePoint 2010**:按一下 **站台動作**在您的網站首頁的左上角。  
  
    2.  按一下 **[更多選項]**。  
  
    3.  在文件庫下，按一下 **[PowerPivot 圖庫]**。  
  
    1.  **SharePoint 2013**:按一下設定圖示![SharePoint 設定](../media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")。 按一下 **[網站內容]**。  
  
    2.  按一下 **[新增應用程式]**。  
  
    3.  按一下 [PowerPivot 圖庫] 。  
  
2.  輸入文件庫的名稱。 請務必包含描述性資訊，以協助使用者將此文件庫識別為 PowerPivot 活頁簿和 Reporting Services 報表的豐富預覽。  
  
3.  按一下 [建立] 。  
  
4.  要求伺服陣列或服務管理員將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫新增為 Excel Service 的信任位置。 如果使用者為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料重新整理設定活頁簿，就需要這個步驟以避免錯誤。 如需有關這項工作的詳細資訊，請參閱 <<c0> [ 在管理中心建立 PowerPivot 網站的信任的位置](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫文件庫的連結會出現在目前網站的導覽 [快速啟動] 窗格中。  
  
 如果您為不同的網站集合或個別網站強制執行不同的權限，則可以建立其他的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫。  
  
##  <a name="customize"></a> 自訂 PowerPivot 圖庫文件庫  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫是 SharePoint 文件庫。 因此，您可以在 SharePoint 中使用標準文件庫工具，以變更文件庫設定，或是使用文件庫中的個別文件。 您建立的每個文件庫都可以獨立自訂，以使用不同的檢視或文件庫設定。  
  
 您可以修改排序次序和篩選，以變更活頁簿出現在清單中的位置。 依預設，會將文件依加入的順序列出，上次發行的文件會出現在清單的底部。 在發行文件之後，該文件會保留它在清單中的位置。 更新和重新發行文件後，會更新它在清單中的位置。  
  
 您無法啟用或停用特定文件的預覽。 快照服務會根據相同文件庫中的 PowerPivot 活頁簿，針對所有 PowerPivot 活頁簿與 Reporting Services 報表產生預覽影像。 擁有文件之「檢視」權限的所有使用者都可以檢視這些影像。  
  
 您無法擴充 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫以提供其他文件類型的預覽。 只有包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的 Excel 2010 活頁簿或 SQL Server 2008 R2 Reporting Services 報表支援預覽。  
  
 您無法變更控制文件來源資訊的設定。 顯示有關個別文件的事實 (例如加入活頁簿或上次修改活頁簿的人員)，是由無法修改的一組固定資料行所決定。  
  
#### <a name="change-sort-order-add-filters-or-limit-the-number-of-documents"></a>變更排序次序、加入篩選，或限制文件的數目  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫永遠會顯示「上次修改」與「建立者」值。 您無法停用這些資料行。 您無法啟用文件庫的其他資料行。請使用下列指示來變更排序次序、加入篩選，或是限制可見的文件數目。  
  
1.  在 SharePoint 網站中，開啟 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫。  
  
2.  在功能區中，按一下 **[文件庫]**。  
  
3.  **SharePoint 2010：** 在 自訂檢視中，按一下**修改此檢視**。  
  
     **SharePoint 2013:** 在 **的 管理檢視**，按一下**修改檢視**。  
  
4.  在 [排序] 中，指定將用來決定活頁簿會如何出現在清單中的準則。 依預設，文件會按照加入的順序列出。  
  
5.  在 [篩選] 中，指定將用來根據在資料行上設定的條件值，來顯示或隱藏活頁簿的準則。 例如，您可能會想要隱藏在特定日期之前所建立的全部活頁簿。  
  
6.  在 [項目限制] 中，指定適用於包含非常大量文件之 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫文件庫的選項。 您可以限制出現在清單中的項目實際數目，或是以批次方式來顯示項目。  
  
7.  按一下 **[確定]** 儲存您的變更。  
  
####  <a name="bkmk_hide_refresh_button"></a> 停用或隱藏重新整理按鈕  
 您無法隱藏 **[管理資料重新整理]** 按鈕。 但如果使用者沒有足夠的權限，就會停用此按鈕。  
  
 ![as_powerpivot_refresh_manage_reresh](../media/as-powerpivot-refresh-manage-reresh.gif "as_powerpivot_refresh_manage_reresh")  
  
 活頁簿擁有者或作者必須具備 **[參與]** 權限，才能排程活頁簿的資料重新整理。 具有 「 參與 」 權限的使用者可以開啟並編輯活頁簿的資料重新整理組態頁面來指定認證和排程來重新整理資料的資訊。  
  
 因此，只有 **[檢視]** 或 **[讀取]** 權限等級的使用者將無法存取此重新整理按鈕。 重新整理按鈕看得到，但是已停用。 如需詳細資訊，請參閱 [SharePoint 2013 的使用者權限與權限等級](https://technet.microsoft.com/library/cc721640.aspx)。  
  
##  <a name="switch"></a> 切換至劇場檢視或圖庫檢視  
 預覽會根據您設定文件庫檢視的方式而有所不同。 在 [組件庫] 檢視中，您可以將滑鼠指標停留在活頁簿中的個別工作表上，讓工作表成為預覽區域中的焦點。  
  
 ![GMNI_ReportGallery](../media/gmni-reportgallery.gif "GMNI_ReportGallery")  
  
 下表描述呈現每個預覽頁面之縮圖草圖的不同版面配置：  
  
|檢視|描述|  
|----------|-----------------|  
|圖庫檢視 (預設值)|圖庫是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫的預設檢視。 預覽會顯示在左邊。 預覽旁邊會顯示每個工作表的小型縮圖，由左至右循序排列。|  
|所有文件|這是文件庫的標準版面配置。 您可以選擇此檢視來管理個別的文件，或以清單格式來檢視文件庫內容。<br /><br /> 使用此檢視來編輯屬性、刪除或移動個別的文件。<br /><br /> 如果您啟用版本控制，必須使用此檢視來檢查文件庫內外的文件。|  
|劇場檢視和浮動切換檢視|如果您展示少數相關文件，這些都是效果最佳的特殊檢視。 完整的縮圖輪替包括文件庫中所有文件中的所有頁面。 如果您有大量的文件，這些檢視對想要尋找或開啟特定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的使用者來說，可能就不太實用。<br /><br /> 劇場檢視：[預覽] 區域會置中。 每個工作表的小型縮圖都會顯示頁面兩側下角。<br /><br /> 浮動切換檢視：[預覽] 區域會置中。 緊接在目前縮圖前後的縮圖與預覽區域相鄰。|  
  
### <a name="switch-to-a-different-view"></a>切換到不同的檢視  
  
1.  在 SharePoint 網站中，開啟 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫。  
  
2.  在功能區中，按一下 **[文件庫]**。  
  
3.  在 [自訂] 檢視的 [管理檢視] 中，從清單選取您要使用的檢視。 預先設計好的檢視包括 [圖庫]、[劇場] 和 [浮動切換]。 或者，如果您要移動、刪除或管理文件庫中的文件，您可以選擇 [所有文件]。  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解 PowerPivot for SharePoint 安裝](../../sql-server/install/troubleshoot-a-powerpivot-for-sharepoint-installation.md)   
 [使用 PowerPivot 圖庫](use-power-pivot-gallery.md)   
 [在管理中心建立 PowerPivot 網站的信任的位置](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [刪除 PowerPivot 圖庫](delete-power-pivot-gallery.md)  
  
  
