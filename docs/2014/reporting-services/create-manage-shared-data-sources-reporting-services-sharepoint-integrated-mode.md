---
title: 建立和管理共用的資料來源 (SharePoint 整合模式的 Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], shared data sources
- shared data sources [Reporting Services]
ms.assetid: 2d3428e4-a810-4e66-a287-ff18e57fad76
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: fdfcdae32c4709a19833612e16a4956f76c78c5f
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295126"
---
# <a name="create-and-manage-shared-data-sources-reporting-services-in-sharepoint-integrated-mode"></a>建立及管理共用資料來源 (SharePoint 整合模式的 Reporting Services)
  當您從 SharePoint 文件庫執行報表時，可以在報表內部或連結到報表的外部檔案中定義連接資訊。 如果連接資訊內嵌於報表中，它就稱為自訂資料來源。 如果連接資訊定義於外部檔案中，它就稱為共用資料來源。 外部檔案可以是報表伺服器資料來源 (.rsds) 檔案或 Office 資料連線 (.odc) 檔案。  
  
 .rsds 檔類似 .rds 檔，但結構描述不同。 若要建立 .rsds 檔，您可以將 .rds 檔從報表設計師或模型設計師中發行到 SharePoint 文件庫 (便會根據原始 .rds 檔建立新的 .rsds 檔)。 或者，您可以在 SharePoint 網站的文件庫中建立新檔案。  
  
 當您建立或發行共用資料來源之後，就可以編輯連接屬性，而且如果已經不需要，還可以刪除該檔案。 刪除共用資料來源之前，您應該先判斷是否有報表和報表模型使用此共用資料來源。 您可以檢視參考到共用資料來源的相依項目來判斷。  
  
 雖然相依項目清單會告訴您是否有項目參考到共用資料來源，但是並不會告訴您此項目目前是否使用中。 若要判斷共用資料來源或模型目前是否使用中，您可以檢閱報表伺服器電腦上的記錄檔。 如果您無法存取這些記錄檔，或者這些檔案沒有包含所需的資訊，請考慮在您判斷報表的實際狀態時，將報表移至無法存取的資料夾。  
  
### <a name="to-create-a-shared-data-source-rsds-file-sharepoint-2010"></a>若要建立共用資料來源 (.rsds) 檔案 (SharePoint 2010)  
  
1.  按一下文件庫功能區上的 [文件] 索引標籤。  
  
2.  在 [新增文件] 功能表上，按一下 [報表資料來源]  
  
    > [!NOTE]  
    >  如果您沒有在功能表上看見 [報表資料來源] 項目，表示報表資料來源內容類型尚未啟用。 如需詳細資訊，請參閱 <<c0> [ 將報表伺服器內容類型加入至文件庫&#40;以 SharePoint 整合模式的 Reporting Services&#41;](../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)。</c0>  
  
3.  在 [名稱] 中，輸入 .rsds 檔的描述性名稱。  
  
4.  在 [資料來源類型] 的清單中，選取資料來源的類型。 如需詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
5.  在 [連接字串] 中，指定資料來源的指標以及其他建立外部資料來源連線必要的任何設定。 您所使用的資料來源類型會決定連接字串的語法。 如需詳細資訊和範例，請參閱 <<c0> [ 資料連接、 資料來源和 Reporting Services 中的連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
6.  在 [認證] 中，指定報表伺服器取得認證來存取外部資料來源的方式。 認證可以針對自動報表處理而儲存、提示、整合或設定。  
  
    -   如果您想要使用開啟報表之使用者的認證來存取資料，請選取 [Windows 驗證 (整合式)]。 如果 SharePoint 網站或伺服陣列使用表單驗證或透過受信任帳戶連接到報表伺服器，請勿選取這個選項。 如果您想要排程這個報表的訂閱或資料處理，請勿選取這個選項。 在針對網域啟用 Kerberos 驗證時，或者資料來源與報表伺服器是在同一部電腦上時，此選項具有最佳的效能。 如果未啟用 Kerberos 驗證，Windows 認證只能傳遞至一部其他電腦。 這表示，如果外部資料來源位於另一部需要其他連接的電腦上，您就會收到錯誤而非所預期的資料。  
  
    -   如果您希望使用者在每次執行報表時輸入自己的認證，請選取 [提示認證]。 如果您想要排程這個報表的訂閱或資料處理，請勿選取這個選項。  
  
    -   如果您想要使用單一認證集來存取這個資料，請選取 [預存認證]。 認證會先經過加密，然後再儲存。 您可以選取決定預存認證之驗證方式的選項。 如果預存認證屬於 Windows 使用者帳戶，請選取 [當做 Windows 認證使用]。 如果您想在資料庫伺服器上設定執行內容，請選取 [設定執行內容到這個帳戶]。 針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫，此選項會設定 SETUSER 函數。 如需詳細資訊，請參閱 [SETUSER &#40;Transact-SQL&#41;](/sql/t-sql/statements/setuser-transact-sql)。  
  
    -   如果您想要在連接字串中指定認證，或是想要使用報表伺服器上設定的最低權限帳戶來執行報表，請選取 [不需要認證]。 如果這個帳戶並未在報表伺服器上設定，系統就會提示使用者輸入認證，而且您針對該報表定義的所有排程作業將不會執行。  
  
7.  如果您想要讓資料來源成為使用中，請選取 [啟用此資料來源]。 如果資料來源已設定，但是非使用中，當使用者嘗試使用以資料來源為基礎的報表時，他們就會看見錯誤訊息。  
  
8.  按一下 [測試連線] 按鈕，驗證資料來源設定。  
  
    > [!NOTE]  
    >  [測試連接] 按鈕不支援 XML 資料來源類型。  
  
9. 按一下 [確定]，儲存建立的共用資料來源。  
  
### <a name="to-view-dependent-items"></a>若要檢視相依項目  
  
1.  開啟包含 .rsds 檔案的文件庫。  
  
2.  指向共用資料來源。  
  
3.  按一下即可顯示向下箭頭，然後選取 [檢視相依項目]。  
  
     若為報表模型，相依項目的清單就會顯示在報表產生器中建立的報表。 若為共用資料來源，相依項目清單可能會同時包括報表和報表模型。  
  
### <a name="to-delete-a-shared-data-source-rsds-file"></a>刪除共用資料來源 (.rsds) 檔案  
  
1.  開啟包含 .rsds 檔案的文件庫。  
  
2.  指向共用資料來源。  
  
3.  按一下即可顯示向下箭頭，然後按一下 [刪除]。  
  
 如果您不小心刪除了想要保留的共用資料來源，可以建立包含相同連接資訊的新共用資料來源。 在您重新建立共用資料來源之後，就必須開啟使用該資料來源的每個報表和模型，然後選取共用資料來源。 新的共用資料來源項目的名稱、認證或連接字串語法可以與之前刪除的資料來源不同。 只要連接解析成相同的資料來源，資料來源屬性可能會與原始值不同。  
  
 刪除報表模型時，請特別小心。 如果您刪除模型，就不能再於報表產生器中，開啟和修改以該模型為基礎的任何報表。 如果您不慎刪除了現有報表所使用的模型，就必須重新產生該模型，重新建立並儲存使用該模型的任何報表，然後重新指定想要使用的任何模型項目安全性。 您不能只是重新產生模型，然後將它附加到現有的報表。  
  
## <a name="see-also"></a>另請參閱  
 [指定報表資料來源的認證及連線資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
