---
title: 使用分頁報表 (Web 入口網站) | Microsoft Docs
description: 了解如何檢視和管理 Web 入口網站內編頁報表的屬性。 此外，了解如何使用報表產生器來建立或編輯編頁報表。
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: fb0bc38f-dc56-4350-8457-cd135c0346e1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1d5c5a6a7b1bd60f066c13a2b06e65dc6ef5f053
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243571"
---
# <a name="working-with-paginated-reports-web-portal"></a>使用分頁報表 (Web 入口網站)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

您可以檢視和管理 Web 入口網站內分頁報表的屬性。 Web 入口網站可以啟動報表產生器來建立或編輯分頁報表。  
   
## <a name="create-a-paginated-report"></a>建立分頁報表  
  
您可以執行以下步驟來建立新的共用資料集。  
  
1.  從功能表列選取 [新增]。  
  
2.  選取 [編頁報表]。  
  
    ![ssRSWebPortal-new-report](../reporting-services/media/ssrswebportal-new-report.png)  
  
3.  將會啟動 [報表產生器]，或提示您下載它。  
  
4.  建置您的報表，然後選取左上方的**儲存**圖示來將分頁報表儲存回報表伺服器。  
  
## <a name="manage-an-existing-paginated-report"></a>管理現有的分頁報表  
  
若要管理現有的分頁報表，您可以執行下列作業。  
  
> [!NOTE]
> 如果您在資料夾中看不到分頁報表，請確定您正在檢視分頁報表。 您可以從入口網站右上角的功能表列選取 [檢視]。 請確定已核取 [編頁報表]。  
  
1.  針對您要管理的資料庫選取**省略符號 (...)** 。  
      
    ![ssRSWebPortal-manage-report1](../reporting-services/media/ssrswebportal-manage-report1.png)  
  
2.  選取 [管理] 會開啟編輯畫面。  
    
    ![ssRSWebPortal-manage-report2](../reporting-services/media/ssrswebportal-manage-report2.png)  
  
## <a name="properties"></a>屬性  
  
在 [屬性] 畫面上，您可以變更分頁報表的 [名稱] 和 [描述]。 您也可以 [刪除]、[移動]、[建立連結報表]、[在報表產生器中編輯]、[下載] 或 [取代]。  
    
![ssRSWebPortal-report-properties](../reporting-services/media/ssrswebportal-report-properties.png)  
   
## <a name="parameters"></a>參數  
  
您可以修改分頁報表的現有參數。 若要加入新的參數，您必須在報表產生器或 SQL Server Data Tools 中編輯報表。  
  
![ssRSWebPortal-report-parameters](../reporting-services/media/ssrswebportal-report-parameters.png)  
   
## <a name="data-source"></a>資料來源  
您可以指向共用資料來源，或輸入自訂資料來源的連接資訊。  
  
![ssRSWebPortal-report-datasource](../reporting-services/media/ssrswebportal-report-datasource.png)  
  
下列選項是用來指定自訂資料來源。  
  
**型別**  
  
指定用來處理資料來源之資料的資料處理延伸模組。 如需內建資料延伸模組的清單，請參閱 [Reporting Services (SSRS) 支援的資料來源]。 其他的資料處理延伸模組可向協力廠商索取。  
  
**連接字串**  
  
指定報表伺服器用來連接至資料來源的連接字串。 連接類型決定您應該使用的語法。 例如，XML 資料處理延伸模組的連接字串是 XML 文件的 URL。 在大部分狀況下，一般連接字串會指定資料庫伺服器和資料檔案。 下列範例將說明用來連接到名為 MyData 之 SQL Server 資料庫的連接字串：  
  
`data source=(a SQL Server instance);initial catalog=MyData`
  
連接字串可設定為運算式，以便於執行階段指定資料來源。 資料來源運算式是在報表設計師的報表中定義的。 Web 入口網站中無法定義、檢視及修改資料來源運算式。 不過，您可以按一下 **[覆寫預設值]** 以輸入靜態連接字串來取代資料來源運算式。 如果您想要切換回運算式，請按一下 [還原為預設值]。 報表伺服器會儲存原始的連接字串，您需要時即可還原。 若要使用資料來源運算式，您必須使用原本在報表中發行的資料來源連接資訊。 共用資料來源不支援在連接字串中使用運算式。  
  
**認證**  
  
您可以指定決定如何取得認證的選項。  
  
> [!IMPORTANT]
> 如果連接字串中有提供認證，則此章節中所提供的選項和值將會被忽略。 請注意，如果您在連接字串上指定認證，這些值就會以純文字的形式顯示給檢視此頁面的所有使用者查看。  
  
**作為檢視報表的使用者**  
  
使用目前使用者的 Windows 認證來存取資料來源。 當用來存取資料來源的認證與用來登入網路網域的認證相同時，請選取此選項。 在針對網域啟用 Kerberos 驗證時，或者資料來源與報表伺服器是在同一部電腦上時，此選項具有最佳的效能。 如果未啟用 Kerberos，無法將 Windows 認證傳遞給其他服務或遠端電腦。 如果需要其他電腦連線，您會收到錯誤而不是預期的資料。  
  
報表伺服器管理員可以停用使用 Windows 整合式安全性來存取報表資料來源的功能。 如果此值呈現灰色，表示這項功能無法使用。  
  
如果您打算要排程或訂閱這個報表，請勿使用這個選項。 已排程或自動報表處理需要使用無需使用者輸入或目前使用者安全性內容即可取得的認證。 只有預存認證會提供這項功能。 因此，如果報表是針對 Windows 整合式安全性認證類型所設定，報表伺服器就會讓您無法排程報表或訂閱處理。 如果您針對已經訂閱或具有排程作業的報表選擇此選項，則訂閱和排程作業將會停止。  
  
**使用這些認證**  
  
在報表伺服器資料庫中儲存加密的使用者名稱和密碼。 選取此選項即可自動執行報表 (例如，由排程或事件起始而不是由使用者的動作起始的報表)。   
  
您也可以選擇此項目的認證類型。 Windows 驗證 (Windows 使用者名稱和密碼) 或特定資料庫認證 (資料庫使用者名稱和密碼) (如 SQL 驗證)。  
  
如果帳戶是 Windows 認證，您所指定的帳戶必須在主控報表所使用資料來源的電腦上擁有本機登入權限。  
  
選取 [使用這些認證登入，但接著嘗試模擬使用者檢視報表]**** 允許委派認證，但是只有在資料來源支援模擬時才應該選取此選項。 若是 SQL Server 資料庫，此選項會設定 SETUSER 函數。 針對 Analysis Services，這會使用 EffectiveUserName。  
  
**提示檢視報表的使用者輸入認證**  
  
每一位使用者都必須輸入使用者名稱和密碼，才可以存取資料來源。 您可以定義要求使用者認證的提示文字。 例如，「輸入使用者名稱和密碼，以存取資料來源。」  
  
您也可以選擇此項目的認證類型。 Windows 驗證 (Windows 使用者名稱和密碼) 或特定資料庫認證 (資料庫使用者名稱和密碼) (如 SQL 驗證)。  
  
**未使用任何認證**  
  
這可讓您不提供資料來源的任何認證。 如果資料來源需要使用者登入，則選擇此選項將沒有作用。 只有當資料來源連接不需要使用者認證時，才應該選擇此選項。  
  
若要使用這個選項，您先前必須已針對報表伺服器設定自動執行帳戶。 當認證的其他進程無法使用時，自動執行帳戶就會用來連接至外部資料來源。 如果您指定了這個選項，但是沒有設定帳戶，報表資料來源的連接將會失敗，而且報表處理將不會進行。 如需此帳戶的詳細資訊，請參閱 [設定自動執行帳戶 (SSRS 組態管理員)](../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
## <a name="subscriptions"></a>訂用帳戶  
Reporting Services 訂閱是在特定時間，或是為了回應某個事件時，以您指定的檔案格式所傳遞之報表組態。 例如，在每個星期三將 MonthlySales.rdl 報表以 Microsoft Word 文件儲存至檔案共用。 訂閱可用於排程及自動化報表的傳遞，並可搭配一組特定的報表參數值。 如需詳細資訊，請參閱[使用訂用帳戶](working-with-subscriptions-web-portal.md)。
  
![ssRSWebPortal-report-subscription1](../reporting-services/media/ssrswebportal-report-subscription1.png)
   
## <a name="dependent-items"></a>相依項目  
使用 [相依項目] 頁面即可檢視參考此報表的項目清單。 每個項目類型的圖示都會表示其用途。 您接著可以選取每個項目上的**省略符號 (...)** ，進一步管理這些項目。  
  
## <a name="caching"></a>Caching  
您有幾個選項可以快取分頁報表的資料。 先從簡單的選取步驟開始。  
  
1.  [永遠以最新的資料執行此報表] 會在每次執行報表時針對資料來源進行查詢。 這會讓依需求報表包含最新的資料。 每次開啟包含新查詢結果的報表時，都會建立報表的新執行個體。 使用此方法時，如果十位使用者同時開啟報表，則會傳送十個查詢至資料來源進行處理。  
  
2.  [快取此報表的複本並在可用時加以使用]**** 會將資料的暫存複本置於快取中，供之後使用。 快取通常會改善效能，因為資料是從快取傳回，而非再次執行資料集查詢。 使用此方法，如果有十位使用者開啟報表，則只有第一個要求會對資料來源發出查詢。 然後報表會快取，其餘九個使用者則檢視快取的報表。  
  
3.  [永遠針對預先產生的快照集執行此報表] 將快取一段指定時段的報表配置和資料。 您可以將報表以報表快照集的形式執行，以避免在任意時間 (例如，在排程備份期間) 執行報表。 快照集可以定期重新整理。 [深入了解]  
  
![ssRSWebPortal-report-caching1](../reporting-services/media/ssrswebportal-report-caching1.png)  
   
選取 [快取此報表的複本並在可用時加以使用] 會顯示更多選項。  
  
![ssRSWebPortal-report-caching2](../reporting-services/media/ssrswebportal-report-caching2.png)  

如需詳細資訊，請參閱[使用快照集](working-with-snapshots-web-portal.md)。
  
### <a name="cache-expiration"></a>快取到期  
  
您可以控制是否要讓分頁報表的快取在一段時間後到期，您也可以選擇用排程來控制。 您可以使用共用排程。  
  
> [!NOTE]
> 這不會重新整理快取。  
  
### <a name="cache-refresh-plans"></a>快取重新整理計劃  
  
您可以使用 [快取重新整理計劃] 來建立排程，以供預先載入含分頁報表之資料暫存複本的快取。 重新整理計劃包括排程和選項，可指定或覆寫參數的值。 您不能覆寫標示為唯讀的參數值。 您可以建立並使用多個重新整理計劃。  
   
可讓您加入、刪除、變更快取重新整理計劃之分頁報表的預設角色指派有：[內容管理員]、[我的報表] 和 [發行者]。  
  
套用上述的快取選項之後，您可以接著定義快取重新整理計劃。 若要這麼做，請在套用快取設定之後，選取顯示的 [管理重新整理計劃] 連結。 隨即會顯示 [快取重新整理計劃] 頁面。   
  
若要建立新的快取重新整理計劃，選取 [新增快取重新整理計劃]。 接下來，您可以輸入計劃的名稱並指定排程。 如果資料集已定義參數，則您可以看到它們列出且可為其提供值，除非它們被標示為唯讀。  
  
當您完成之後，即可選取 [建立快取重新整理計劃]。  
  
![ssRSWebPortal-report-caching3](../reporting-services/media/ssrswebportal-report-caching3.png)  
  
> [!NOTE]
> 必須正在執行 SQL Server Agent 才能建立快取重新整理計劃。  
  
您接著可以 [編輯] 或 [刪除] 列出的計劃。 當只有選取一個快取重新整理計劃時，才會啟用 [從現有的新增] 選項。 這個選項會建立從原始計劃複製的新重新整理計劃。 [快取重新整理計劃] 頁面開啟時會預先填入所選取計劃的詳細資料。 接著，您就可以修改重新整理計劃選項，然後使用新的描述儲存該計劃。  
  
## <a name="history-snapshots"></a>記錄快照集  
  
使用 [記錄快照集] 頁面來檢視產生和儲存一段時間的報表快照集。 依據設定的選項，報表記錄可能只包含最近的快照集。  
  
報表記錄一定是在資源報表的內容中提供檢視的。 您無法在某個位置中檢視報表伺服器上所有報表的記錄。  
  
若要產生快照集，報表必須可以自動執行 (亦即它必須使用預存認證；參數化的報表必須包含所有參數的預設參數值)。 可以手動或以排程作業來產生快照集。   
  
按一下報表記錄快照集即可檢視該快照集。 報表記錄中顯示的快照集只能以建立日期和時間來區分。 沒有視覺指示可以區分快照集是回應排程而建立或是手動作業所建立。  
  
## <a name="security"></a>安全性  
使用 [安全性屬性] 頁面來檢視或修改安全性設定，以決定報表的存取權。 此頁面適用於您有權保護的項目。  
  
透過指定群組或使用者可執行的工作的角色指派來定義項目的存取權。 角色指派含有一個使用者或群組名稱，以及一個或多個指定工作集合的角色定義。  
  
**編輯項目安全性**  
  
選取即可變更定義目前項目安全性的方式。

## <a name="next-steps"></a>後續步驟

[入口網站](../reporting-services/web-portal-ssrs-native-mode.md)  
[使用共用資料集](../reporting-services/work-with-shared-datasets-web-portal.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
