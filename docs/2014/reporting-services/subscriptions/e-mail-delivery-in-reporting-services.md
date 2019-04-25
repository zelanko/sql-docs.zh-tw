---
title: Reporting Services 中的電子郵件傳遞 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 45e72fe3c163f05f283965beb5fb3cf6ce62c50e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62510942"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Reporting Services 中的電子郵件傳遞
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含了電子郵件傳遞延伸模組，可讓您透過電子郵件傳送報表給個別使用者或群組。 您可以透過 Reporting Services 組態管理員並藉由編輯 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態檔，設定電子郵件傳遞延伸模組。  
  
 若要透過電子郵件散發或接收報表，您可以定義標準訂閱或資料驅動訂閱。 您一次只能訂閱或散發一個報表。 您無法建立在單一電子郵件訊息中傳遞多個報表的訂閱。 如需有關訂用帳戶的詳細資訊，請參閱[建立、 修改和刪除標準訂用帳戶&#40;原生模式的 Reporting Services&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式&#124;SharePoint 2010 和 SharePoint 2013<br /><br /> **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
## <a name="e-mail-delivery-options"></a>電子郵件傳遞選項  
 報表伺服器電子郵件傳遞可以利用下列方式傳遞報表：  
  
-   傳送通知和超連結到產生的報表。  
  
-   在電子郵件訊息的 [主旨:] 傳送通知。 依預設，訂閱定義中的 [主旨:] 包含下列變數，處理訂閱時，會以報表特定資訊取代這些變數：  
  
     **@ReportName** 指定報表的名稱。  
  
     **@ExecutionTime** 指定報表執行的時間。  
  
     您可以將這些變數與靜態文字結合，或者修改每個訂閱 [主旨:] 中的文字。  
  
-   傳送內嵌的或附加的報表。 轉譯格式和瀏覽器會決定是否要內嵌或附加報表。  
  
     如果您的瀏覽器支援 HTML 4.0 與 MHTML，而且您選擇網頁封存轉譯格式，則報表會內嵌為訊息的一部分。 所有其他轉譯格式 (CSV、PDF 等等) 均以附加檔案傳遞報表。 您可以在 RSReportServer 組態檔中停用此功能。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在傳送報表之前，不會檢查附加檔案或訊息的大小。 如果附加檔案或訊息超過郵件伺服器所允許的上限，將不會傳遞報表。 如果是大型報表，請選擇其他傳遞選項之一 (例如 URL 或通知)。  
  
 您可以設定傳遞選項，來決定建立訂閱時如何傳遞報表。 例如，您若是在訂閱中選取 [包含連結]，則電子郵件訊息包含連結到報表的超連結。  
  
## <a name="role-based-e-mail-settings"></a>以角色為基礎的電子郵件設定  
 您訂閱報表時所使用的電子郵件傳遞設定，會依您的角色包含的是「管理個別訂閱」工作或「管理所有訂閱」工作而異。  
  
|工作|可用的設定|  
|----------|------------------------|  
|管理個別訂閱|顯示讓使用者可自動化並傳遞報表給自己的欄位。 在此模式下，接受電子郵件別名的欄位無法使用。|  
|管理所有訂閱|顯示支援全域散發的欄位，包括 [收件者:]、[副本:]、[密件副本:] 和 [回覆至:] 欄位，提供更多方式傳送報表給更多訂閱者。 電子郵件別名欄位的可用性是透過 RSReportServer 組態檔設定定義。|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>在訂閱中指定電子郵件位址  
 如果您是在內部網路散發報表，而且使用的是通往 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange 伺服器的 SMTP 閘道，請輸入電子郵件別名 (就像您傳送電子郵件給同事一樣)。 若要傳遞到外部電子郵件帳戶，請輸入完整電子郵件地址。 如果指定更多電子郵件地址以加入其他人到訂閱中，訂閱者會取得此訂閱所產生的報表完整副本。  
  
 報表伺服器不會驗證電子郵件地址，或從電子郵件伺服器取得電子郵件地址。 您必須事先知道要使用的電子郵件地址。 依預設，您可以利用電子郵件傳送報表給組織內外任何有效的電子郵件帳戶。 但是，可以使用組態設定，將電子郵件傳遞至限制在您依名稱識別的郵件伺服器主機。 如果您想要支援電子郵件傳遞給非組織成員的人，則可以指定其他主機。  
  
 用來傳遞報表的電子郵件訊息，必須從電子郵件伺服器上所定義的電子郵件帳戶傳送。 組態設定會指定電子郵件帳戶。 電子郵件帳戶是供所有藉由電子郵件傳遞延伸模組傳遞之報表所使用的；您無法指定多個帳戶或對個別報表指定不同帳戶。  
  
## <a name="e-mail-server-configuration"></a>電子郵件伺服器組態  
 報表伺服器會透過標準連線來與電子郵件伺服器連接。 並未使用以安全通訊端層 (SSL) 加密的通訊。 電子郵件伺服器必須是與報表伺服器在相同網路中的遠端或本機 Simple Mail Transport Protocol (SMTP) 伺服器。  
  
 如需如何設定原生模式報表伺服器的詳細資訊，請參閱下列內容：  
  
-   [為電子郵件傳遞設定報表伺服器&#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
  
-   [電子郵件設定-Configuration Manager &#40;SSRS 原生模式&#41;](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)  
  
 如需如何設定 SharePoint 模式報表伺服器的詳細資訊，請參閱下列內容：  
  
-   [設定 Reporting Services 服務應用程式的電子郵件 &#40;SharePoint 2010 和 SharePoint 2013&#41;](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
## <a name="see-also"></a>另請參閱  
 [工作和權限](../security/tasks-and-permissions.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [資料驅動訂閱](data-driven-subscriptions.md)   
 [角色指派](../security/role-assignments.md)  
  
  
