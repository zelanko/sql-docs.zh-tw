---
title: Reporting Services 中的電子郵件傳遞 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b2d5f511fe6008801b25f7c93300911851482025
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305042"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Reporting Services 中的電子郵件傳遞
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含了電子郵件傳遞延伸模組，可讓您透過電子郵件傳送報表給個別使用者或群組。 若要透過電子郵件散發報表，您可以 1) 設定報表伺服器的電子郵件傳遞以及 2) 定義標準訂閱或資料驅動訂閱。 單一訂閱無法在單一電子郵件訊息中傳遞多個報表。 不過，您可以建立多個訂閱。  
  
 報表伺服器會透過標準連線來與電子郵件伺服器連接。 並未使用以安全通訊端層 (SSL) 加密的通訊。 電子郵件伺服器必須是與報表伺服器在相同網路中的遠端或本機 Simple Mail Transport Protocol (SMTP) 伺服器。  
  
 如需逐步引導您建立訂閱的詳細步驟，請參閱下方項目︰  
  
-   [建立及管理原生模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
-   [建立及管理 SharePoint 模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
## <a name="e-mail-delivery-options"></a>電子郵件傳遞選項  
 報表伺服器電子郵件傳遞可以利用下列方式傳遞報表  
  
-   傳送通知和超連結到產生的報表。  
  
-   在電子郵件訊息的 [主旨:] 傳送通知。 依預設，訂閱定義中的 [主旨:] 包含下列變數，處理訂閱時，會以報表特定資訊取代這些變數：  
  
     **\@ReportName** 指定報表的名稱。  
  
     **\@ExecutionTime** 指定報表執行的時間。  
  
     您可以將這些變數與靜態文字結合，或者修改每個訂閱 [主旨:] 中的文字。  
  
-   傳送內嵌的或附加的報表。 轉譯格式和瀏覽器會決定是否要內嵌或附加報表。  
  
     如果您的瀏覽器支援 HTML 4.0 與 MHTML，而且您選擇網頁封存轉譯格式，則報表會內嵌為訊息的一部分。 所有其他轉譯格式 (CSV、PDF 等等) 均以附加檔案傳遞報表。 對於原生模式報表伺服器，您可以在 RSReportServer.config 組態檔中停用此功能。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在傳送報表之前，不會檢查附加檔案或訊息的大小。 如果附加檔案或訊息超過郵件伺服器所允許的上限，將不會傳遞報表。 如果是大型報表，請選擇其他傳遞選項之一 (例如 URL 或通知)。  
  
 您可以設定傳遞選項，來決定建立訂閱時如何傳遞報表。 例如，您若是在訂閱中選取 [包含連結]  ，則電子郵件訊息包含連結到報表的超連結。  
  
## <a name="native-mode-role-based-e-mail-settings"></a>原生模式角色型電子郵件設定  
 在原生模式報表伺服器環境中，您所使用的電子郵件傳遞設定會依您的角色包含的是「管理個別訂閱」工作或「管理所有訂閱」工作而異。  
  
|工作|可用的設定|  
|----------|------------------------|  
|管理個別訂閱|顯示讓使用者可自動化並傳遞報表給自己的欄位。 在此模式下，接受電子郵件別名的欄位無法使用。|  
|管理所有訂閱|顯示支援全域散發的欄位，包括 [收件者:]、[副本:]、[密件副本:] 和 [回覆至:] 欄位，提供更多方式傳送報表給更多訂閱者。 電子郵件別名欄位的可用性是透過 RSReportServer 組態檔設定定義。|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>在訂閱中指定電子郵件位址  
 如果您是在內部網路散發報表，而且使用的是通往 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange 伺服器的 SMTP 閘道，請輸入電子郵件別名 (就像您傳送電子郵件給同事一樣)。 若要傳遞到外部電子郵件帳戶，請輸入完整電子郵件地址。 如果指定更多電子郵件地址以加入其他人到訂閱中，訂閱者會取得此訂閱所產生的報表完整副本。  
  
 報表伺服器不會驗證電子郵件地址，或從電子郵件伺服器取得電子郵件地址。 您必須事先知道要使用的電子郵件地址。 依預設，您可以利用電子郵件傳送報表給組織內外任何有效的電子郵件帳戶。 但是，可以使用組態設定，將電子郵件傳遞至限制在您依名稱識別的郵件伺服器主機。 如果您想要支援電子郵件傳遞給非組織成員的人，則可以指定其他主機。  
  
 用來傳遞報表的電子郵件訊息，必須從電子郵件伺服器上所定義的電子郵件帳戶傳送。 組態設定會指定電子郵件帳戶。 電子郵件帳戶是供所有藉由電子郵件傳遞延伸模組傳遞之報表所使用的；您無法指定多個帳戶或對個別報表指定不同帳戶。  
  
## <a name="controlling-e-mail-delivery"></a>控制電子郵件傳遞  
 您可以設定報表伺服器，來限制只能散發電子郵件至特定主機網域。 例如，您可以防止原生報表伺服器將報表傳遞至 **RSReportServer.config** 組態檔中所列網域以外的所有網域。  
  
 您也可以組態組態設定，以隱藏訂閱中的 [收件者]  欄位。 在此情況下，報表只會傳遞給定義訂閱的使用者。 然而，在報表傳送給使用者之後，您無法明確地防止其被轉送。  
  
 控制報表散發最有效的方式，是將報表伺服器設定為只傳送報表伺服器 URL。 報表伺服器使用 Windows 驗證和以角色為基礎的驗證模型，來控制對報表的存取。 如果使用者意外地透過電子郵件接收到未被授權檢視的報表，報表伺服器將不會顯示報表。 如需有關訂閱的詳細資訊，請參閱下方項目。  
  
## <a name="e-mail-server-configuration"></a>電子郵件伺服器組態  
 對於原生模式報表伺服器，您可以透過原生模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員並藉由編輯 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態檔，設定電子郵件傳遞延伸模組。 對於 SharePoint 模式報表伺服器，您可在 SharePoint 管理頁面和 PowerShell 指令碼中設定電子郵件傳遞延伸模組。  
  
 
 如需如何設定原生模式報表伺服器的資訊，請參閱 [電子郵件設定 - Reporting Services 原生模式 (組態管理員)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)
 
 
 如需如何設定 SharePoint 模式報表伺服器的詳細資訊，請參閱下列內容：  
  
  
## <a name="see-also"></a>另請參閱  
 [工作和權限](../../reporting-services/security/tasks-and-permissions.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [資料驅動訂閱](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [角色指派](../../reporting-services/security/role-assignments.md)  
  
  
