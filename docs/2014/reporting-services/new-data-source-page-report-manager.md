---
title: 新增資料來源頁面 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 35563d4c-a3d5-4f95-bf46-605da9dfcbb8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9cc4dda934496bbfa33306537b515870f0de23de
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108181"
---
# <a name="new-data-source-page-report-manager"></a>新增資料來源頁面 (報表管理員)
  使用 [新增資料來源] 頁面來建立共用資料來源項目。 共用資料來源定義外部資料來源的連接。 您可以利用共用資料來源來建立和維護資料來源連接的設定，與使用該資料來源的報表、模型和資料驅動訂閱分開處理。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-new-data-source-page"></a>若要開啟新增資料來源頁面  
  
1.  開啟報表管理員中，然後導覽至您想要在其中建立資料來源的資料夾。  
  
2.  在工具列中，按一下 **[新增資料來源]**。 您必須擁有「內容管理員」權限才能建立共用資料來源。  
  
## <a name="options"></a>選項  
 **名稱**  
 輸入共用資料來源的名稱，可用來識別報表伺服器資料夾階層中的項目。  
  
 **說明**  
 提供有關共用資料來源的資訊。 此描述會顯示在 [內容] 頁面上。  
  
 **在清單檢視中隱藏**  
 選取這個選項可以對正在「報表管理員」中使用清單檢視模式的使用者隱藏共用資料來源。 清單檢視模式是瀏覽報表伺服器資料夾階層時的預設檢視格式。 在清單檢視中，項目名稱和描述會跨頁排列。 替代格式是詳細資料檢視。 詳細資料檢視會省略描述，但會包括項目的其他相關資訊。 雖然在清單檢視中可以隱藏項目，但在詳細資料檢視中則不行。 如果您要限制對某個項目的存取，必須建立角色指派。  
  
 **啟用此資料來源**  
 選取以啟用或停用共用資料來源。 您可以停用共用資料來源，以避免報表處理參考該項目的所有報表和模型。  
  
 **資料來源類型**  
 指定用來處理資料來源之資料的資料處理延伸模組。 報表伺服器包括 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、Oracle、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]、SAP、XML、ODBC 和 OLE DB 的資料處理延伸模組。 其他的資料處理延伸模組可向協力廠商索取。  
  
 如需有關遠端及非 SQL 資料來源支援的詳細資訊，請參閱[支援的 SQL Server 2012 版本的功能](https://go.microsoft.com/fwlink/?linkid=232473)(超連結"<https://go.microsoft.com/fwlink/?linkid=232473>" <https://go.microsoft.com/fwlink/?linkid=232473>) 和[支援的報表資料來源服務&#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
 **連接字串**  
 指定報表伺服器用來連接至資料來源的連接字串。 連接類型決定您應該使用的語法。 例如，XML 資料處理延伸模組的連接字串是 XML 文件的 URL。 在大部分狀況下，一般連接字串會指定資料庫伺服器和資料檔案。  
  
 下列範例說明用來連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 資料庫的連接字串：  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 如需範例和不同的方式，來指定連接字串的相關資訊，請參閱[資料連接、 資料來源和 Reporting Services 中的連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
 **使用連線**  
 指定決定如何取得認證的選項。  
  
> [!IMPORTANT]  
>  如果連接字串中有提供認證，則此章節中所提供的選項和值將會被忽略。 請注意，如果您在連接字串上指定認證，這些值就會以純文字的形式顯示給檢視此頁面的所有使用者查看。  
  
 **執行報表 （使用下列方式連接） 的使用者所提供的認證**  
 系統會提示每一位使用者輸入使用者名稱和密碼，以存取資料來源。 您可以定義要求使用者認證的提示文字。 預設的文字字串是「請輸入使用者名稱和密碼以存取資料來源」。  
  
 如果使用者提供的認證是 Windows 驗證認證，請選取 [連接到資料來源時作為 Windows 認證]  。 如果您是使用資料庫驗證 (例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證)，請勿選取此核取方塊。  
  
 **認證安全地儲存在報表伺服器 （使用下列方式連接）**  
 在報表伺服器資料庫中儲存加密的使用者名稱和密碼。 選擇此選項即可自動執行報表 (例如，由排程或事件啟動而不是由使用者動作啟動的報表)。 如果您要使用預設安全性，使用者名稱就必須是 Windows 網域帳戶。 以此格式指定帳戶：\<網域 >\\< 使用者名稱\>。 您所指定的帳戶必須在主控報表所使用之資料來源的電腦上擁有本機登入權限。  
  
 如果認證是 Windows 驗證認證，請選取 **[連接到資料來源時作為 Windows 認證]** 。 如果您是使用資料庫驗證 (例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證)，請勿選取此核取方塊。  
  
 如果您要使用資料庫驗證，請選取 **[連接到資料來源後，模擬已驗證的使用者]** 以便允許資料庫認證的委派，但是只有在資料庫伺服器支援模擬時才應該選取此選項。 針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫，此選項會設定 SETUSER 函數。  
  
 **Windows 整合式的安全性 （使用下列方式連接）**  
 使用目前使用者的 Windows 認證來存取資料來源。 當用來存取資料來源的認證與用來登入網路網域的認證相同時，請選擇此選項。 在針對網域啟用 Kerberos 驗證時，或者資料來源與報表伺服器是在同一部電腦上時，此選項具有最佳的效能。 如果未啟用 Kerberos 驗證，Windows 認證可以傳遞至一部其他電腦。 如果需要其他電腦連線，您會收到錯誤而不是預期的資料。  
  
 報表伺服器管理員可以停用使用 Windows 整合式安全性來存取報表資料來源的功能。 如果此值呈現灰色，表示這項功能無法使用。  
  
 如果您打算要排程或訂閱這個報表，請勿使用這個選項。 已排程或自動報表處理需要使用無需使用者輸入或目前使用者安全性內容即可取得的認證。 只有預存認證會提供這項功能。 因此，如果報表是針對 Windows 整合式安全性認證類型所設定，報表伺服器就會讓您無法排程報表或訂閱處理。 如果您針對已經訂閱或具有排程作業的報表選擇此選項，則訂閱和排程作業將會停止。  
  
 **不需要認證 （使用連接）**  
 指定不需要認證就可以存取資料來源。 請注意，如果資料來源需要使用者登入，則選擇此選項將沒有作用。 只有當資料來源連接不需要使用者認證時，才應該選擇此選項。  
  
 若要使用這個選項，您先前必須已針對報表伺服器部署設定了自動執行帳戶。 當認證的其他來源無法使用時，自動執行帳戶就會用來連接至外部資料來源。 如果您指定了這個選項，但是沒有設定帳戶，報表資料來源的連接將會失敗，而且報表處理將不會進行。 如需有關此帳戶的詳細資訊，請參閱 <<c0> [ 設定自動執行帳戶&#40;SSRS 組態管理員&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。</c0>  
  
 **確定**  
 按一下即可儲存您的變更。  
  
## <a name="see-also"></a>另請參閱  
 [建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [資料連接、 資料來源和 Reporting Services 中的連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [內容頁面 &#40;報表管理員&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [建立、修改和刪除共用資料來源 &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [指定報表資料來源的認證及連線資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
