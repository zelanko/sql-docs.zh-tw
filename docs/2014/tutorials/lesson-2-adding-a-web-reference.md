---
title: 第2課：加入 Web 參考 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a2c2b8b8-6b13-45ca-ab3b-1582447b6807
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: dd4b9edc8c054a7fa2ec84bdc8d892e5b5a903a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63316013"
---
# <a name="lesson-2-adding-a-web-reference"></a>第 2 課：加入 Web 參考
  Web 服務探索是用戶端用來尋找 Web 服務及取得服務描述的程序。 
  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的 Web 服務探索程序牽涉到依照預先定義的演算法來詢問網站。 此程序的目的是尋找服務描述，也就是使用 Web 服務描述語言 (WSDL) 的 XML 文件集。  
  
 服務描述所描述的是可用的服務以及如何與這些服務互動。 若沒有服務描述，即無法與 Web 服務建立程式化的互動。  
  
 您的應用程式必須有與 Web 服務通訊的方式，以及在執行階段尋找 Web 服務的方式。 Web 服務藉由產生與 Web 服務互動，同時提供 Web 服務本機表示的 Proxy 類別，將 Web 參考加入您的專案中。 如需詳細資訊，請參閱 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 文件集中的＜HOW TO：產生 XML Web Service Proxy＞。  
  
### <a name="to-add-a-web-reference"></a>若要加入 Web 參考  
  
1.  在 [**專案**] 功能表上，按一下 [**加入服務參考**]。  
  
2.  在 [**加入服務參考**] 對話方塊中，按一下 [ **Advanced**]。  
  
3.  在 [**服務參考設定**] 對話方塊中，按一下 [**加入 Web 參考**]。  
  
4.  在 [**加入 Web 參考**] 對話方塊的 [ http://localhost/reportserver/reportservice2010.asmx **url** ] 方塊中，輸入 url 以取得報表伺服器 Web 服務的服務描述，例如。 然後**按一下 [執行] 按鈕，以**取得有關 Web 服務的資訊。  
  
     \- 或 -  
  
     如果報表伺服器 Web 服務存在於本機電腦上，請按一下 [瀏覽器] 窗格中的 [**本機電腦上的 Web 服務**] 連結。 然後按一下所提供清單中的 ReportService2010 Web 服務連結。  
  
5.  在 [ **web 參考名稱**] 方塊中，將 web 參考重新命名為 ReportService2010，這是您將用於此 web 參考的命名空間。  
  
6.  按一下 [**加入參考**]，為目標 Web 服務新增 Web 參考。  
  
     
  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 會下載服務描述，並產生聯繫應用程式和報表伺服器 Web 服務的 Proxy 類別。 您也必須加入 <xref:System.Web.Services> 命名空間的參考，才能讓 Web 參考運作。  
  
7.  在 [專案] 功能表上，按一下 [**加入參考**]。  
  
8.  在 [**加入參考**] 對話方塊的 [ **.net** ] 索引標籤中，選取 [ **System.web**]，然後按一下 **[確定]**。  
  
 如需詳細資訊，請參閱[存取 SOAP API](../reporting-services/report-server-web-service/accessing-the-soap-api.md)。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器 Web 服務](../reporting-services/report-server-web-service/report-server-web-service.md)   
 [第3課：存取 Web 服務](../../2014/tutorials/lesson-3-accessing-the-web-service.md)   
 [使用 Visual Basic 或 Visual C&#35; &#40;SSRS 教學課程來存取報表伺服器 Web 服務&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  
