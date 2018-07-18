---
title: 第 2 課： 加入 Web 參考 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a2c2b8b8-6b13-45ca-ab3b-1582447b6807
caps.latest.revision: 29
author: craigg-msft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff0efdd840ee2f4efb0da802da64494640911b80
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275624"
---
# <a name="lesson-2-adding-a-web-reference"></a>第 2 課：加入 Web 參考
  Web 服務探索是用戶端用來尋找 Web 服務及取得服務描述的程序。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的 Web 服務探索程序牽涉到依照預先定義的演算法來詢問網站。 此程序的目的是尋找服務描述，也就是使用 Web 服務描述語言 (WSDL) 的 XML 文件集。  
  
 服務描述所描述的是可用的服務以及如何與這些服務互動。 若沒有服務描述，即無法與 Web 服務建立程式化的互動。  
  
 您的應用程式必須有與 Web 服務通訊的方式，以及在執行階段尋找 Web 服務的方式。 Web 服務藉由產生與 Web 服務互動，同時提供 Web 服務本機表示的 Proxy 類別，將 Web 參考加入您的專案中。 如需詳細資訊，請參閱 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 文件集中的＜HOW TO：產生 XML Web Service Proxy＞。  
  
### <a name="to-add-a-web-reference"></a>若要加入 Web 參考  
  
1.  在 **專案**功能表上，按一下**加入服務參考**。  
  
2.  在 [**加入服務參考**] 對話方塊中，按一下**進階**。  
  
3.  在 [**服務參考設定**] 對話方塊中，按一下**加入 Web 參考**。  
  
4.  在  **URL**的方塊**加入 Web 參考**方塊中，輸入可取得服務描述的報表伺服器 Web 服務，例如 URL http://localhost/reportserver/reportservice2010.asmx。 然後按一下**移** 按鈕，擷取 Web 服務的相關資訊。  
  
     \- 或 -  
  
     如果報表伺服器 Web 服務存在本機電腦上，按一下**本機電腦上的 Web 服務**瀏覽器窗格中的連結。 然後按一下所提供清單中的 ReportService2010 Web 服務連結。  
  
5.  在  **Web 參考名稱**方塊中，Web 將參考重新命名為 ReportService2010，這是您將使用此 Web 參考的命名空間。  
  
6.  按一下 **加入參考**新增目標 Web 服務的 Web 參考。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 會下載服務描述，並產生聯繫應用程式和報表伺服器 Web 服務的 Proxy 類別。 您也必須加入 <xref:System.Web.Services> 命名空間的參考，才能讓 Web 參考運作。  
  
7.  在 專案 功能表中，按一下 **加入參考**。  
  
8.  在**加入參考**對話方塊中，於 **.NET**索引標籤上，選取**System.Web.Services**，然後按一下**確定**。  
  
 如需詳細資訊，請參閱[存取 SOAP API](../reporting-services/report-server-web-service/accessing-the-soap-api.md)。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器 Web 服務](../reporting-services/report-server-web-service/report-server-web-service.md)   
 [第 3 課： 存取 Web 服務](../../2014/tutorials/lesson-3-accessing-the-web-service.md)   
 [存取報表伺服器 Web 服務使用 Visual Basic 或 Visual C&#35; &#40;SSRS 教學課程&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  
