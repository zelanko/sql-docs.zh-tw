---
title: 資料來源屬性頁面 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f37edda0-19e6-489e-b544-8751fa6b6cfb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 00bc66f116a489858d6383d90a17e730792e6325
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59941634"
---
# <a name="data-sources-properties-page-report-manager"></a>資料來源屬性頁面 (報表管理員)
  使用 [資料來源] 屬性頁，即可定義目前的報表如何連接到外部資料來源。 您可以覆寫原先隨同報表發行的資料來源連線資訊。 如果報表使用多重資料來源，則每一個資料來源在屬性頁中各有它自己的區段。 資料來源依其報表中定義的排序來列示。  
  
 指定報表使用的資料來源時，可以使用共用資料來源，共用資料來源可與使用它的報表分開來建立和管理。 如果不要使用共用資料來源項目，您就可以定義報表使用的資料來源連接。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-data-sources-properties-page"></a>若要開啟資料來源屬性頁面  
  
1.  開啟報表管理員，然後找出您想要選取資料來源的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]**。 這樣就會開啟該報表的 **[一般]** 屬性頁面。  
  
4.  選取 **[資料來源]** 索引標籤。  
  
## <a name="options"></a>選項。  
 **共用的資料來源**  
 指定報表使用的共用資料來源。 如需建立新的資料來源的詳細資訊，請參閱 <<c0> [ 建立、 刪除或修改共用資料來源&#40;報表管理員&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)。</c0>  
  
 **瀏覽**  
 按一下 **[瀏覽]** ，即可開啟 [資料來源選取] 頁面，此頁面是用來選取共用資料來源。 如需詳細資訊，請參閱 <<c0> [ 資料來源選擇頁面&#40;報表管理員&#41;](../../2014/reporting-services/data-source-selection-page-report-manager.md)。</c0>  
  
 **自訂資料來源**  
 指定報表與資料來源的連接方式。  
  
 下列選項是用來指定自訂資料來源連接。  
  
 **資料來源類型**  
 指定用來處理資料來源之資料的資料處理延伸模組。 如需內建資料延伸模組的清單，請參閱[Reporting Services 所支援的資料來源&#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)。 其他的資料處理延伸模組可向協力廠商索取。  
  
 **連接字串**  
 指定報表伺服器用來連接至資料來源的連接字串。 連接類型決定您應該使用的語法。 例如，XML 資料處理延伸模組的連接字串是 XML 文件的 URL。 在大部分狀況下，一般連接字串會指定資料庫伺服器和資料檔案。 下列範例將說明用來連接到名為 MyData 之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫的連接字串：  
  
 `data source=<a SQL Server instance>;initial catalog=MyData`  
  
 連接字串可設定為運算式，以便於執行階段指定資料來源。 資料來源運算式是在報表設計師的報表中定義的。 「報表管理員」中無法定義、檢視及修改資料來源運算式。 不過，您可以按一下 **[覆寫預設值]** 以輸入靜態連接字串來取代資料來源運算式。 如果您想要切換回運算式，請按一下 **[還原為預設值]**。 報表伺服器會儲存原始的連接字串，您需要時即可還原。 若要使用資料來源運算式，您必須使用原本在報表中發行的資料來源連接資訊。 共用資料來源不支援在連接字串中使用運算式。  
  
 **使用連線**  
 指定決定如何取得認證的選項。  
  
> [!IMPORTANT]  
>  如果連接字串中有提供認證，則此章節中所提供的選項和值將會被忽略。 請注意，如果您在連接字串上指定認證，這些值就會以純文字的形式顯示給檢視此頁面的所有使用者查看。  
  
 **執行報表的使用者所提供的認證**  
 每一位使用者都必須輸入使用者名稱和密碼，才可以存取資料來源。 您可以定義要求使用者認證的提示文字。 預設的文字字串是「請輸入使用者名稱和密碼以存取資料來源」。  
  
 如果使用者提供的認證是 Windows 驗證認證，請選取 [連接到資料來源時作為 Windows 認證]  。 如果您是使用資料庫驗證 (例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證)，請勿選取此核取方塊。  
  
 **安全地儲存在報表伺服器的認證**  
 在報表伺服器資料庫中儲存加密的使用者名稱和密碼。 選取此選項即可自動執行報表 (例如，由排程或事件起始而不是由使用者的動作起始的報表)。 如果您要使用預設安全性，使用者名稱就必須是 Windows 網域帳戶。 以此格式指定帳戶：\<網域 >\\< 使用者名稱\>。 您所指定的帳戶必須在主控報表所使用之資料來源的電腦上擁有本機登入權限。  
  
 如果認證是 Windows 驗證認證，請選取 **[連接到資料來源時作為 Windows 認證]** 。 如果您是使用資料庫驗證 (例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證)，請勿選取此核取方塊。  
  
 請選取 **[連接到資料來源後，模擬已驗證的使用者]** 以便允許認證的委派，但是只有在資料來源支援模擬時才應該選取此選項。 針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫，此選項會設定 SETUSER 函數。  
  
> [!TIP]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]只支援 Windows 帳戶認證。 因此，若為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源，請選取 [連接到資料來源時作為 Windows 認證] 和 [連接到資料來源後，模擬已驗證的使用者] 這兩個選項。  
  
 **Windows 整合式的安全性**  
 使用目前使用者的 Windows 認證來存取資料來源。 當用來存取資料來源的認證與用來登入網路網域的認證相同時，請選取此選項。 在針對網域啟用 Kerberos 驗證時，或者資料來源與報表伺服器是在同一部電腦上時，此選項具有最佳的效能。 若未啟用 Kerberos，Windows 認證可以傳送至其他電腦。 如果需要其他電腦連線，您會收到錯誤而不是預期的資料。  
  
 報表伺服器管理員可以停用使用 Windows 整合式安全性來存取報表資料來源的功能。 如果此值呈現灰色，表示這項功能無法使用。  
  
 如果您打算要排程或訂閱這個報表，請勿使用這個選項。 已排程或自動報表處理需要使用無需使用者輸入或目前使用者安全性內容即可取得的認證。 只有預存認證會提供這項功能。 因此，如果報表是針對 Windows 整合式安全性認證類型所設定，報表伺服器就會讓您無法排程報表或訂閱處理。 如果您針對已經訂閱或具有排程作業的報表選擇此選項，則訂閱和排程作業將會停止。  
  
 **不需要認證**  
 指定不需要認證就可以存取資料來源。 請注意，如果資料來源需要使用者登入，則選擇此選項將沒有作用。 只有當資料來源連接不需要使用者認證時，才應該選擇此選項。  
  
 若要使用這個選項，您先前必須已針對報表伺服器部署設定了自動執行帳戶。 當認證的其他來源無法使用時，自動執行帳戶就會用來連接至外部資料來源。 如果您指定了這個選項，但是沒有設定帳戶，報表資料來源的連接將會失敗，而且報表處理將不會進行。  如需有關此帳戶的詳細資訊，請參閱 <<c0> [ 設定自動執行帳戶&#40;SSRS 組態管理員&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。</c0>  
  
 **Apply**  
 按一下即可儲存您的變更。  
  
## <a name="see-also"></a>另請參閱  
 [管理報表資料來源](report-data/manage-report-data-sources.md)   
 [指定報表資料來源的認證及連接資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
