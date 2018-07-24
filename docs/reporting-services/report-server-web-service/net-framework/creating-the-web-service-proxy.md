---
title: 建立 Web 服務 Proxy | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, proxies
- proxies [Reporting Services]
- XML Web service [Reporting Services], proxies
- Web service [Reporting Services], proxies
- Web references [Reporting Services]
ms.assetid: b1217843-8d3d-49f3-a0d2-d35b0db5b2df
caps.latest.revision: 44
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7cfc77e602a6d5082a9ffc44ed98b1710bcd19e9
ms.sourcegitcommit: 9229fb9b37616e0b73e269d8b97c08845bc4b9f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/13/2018
ms.locfileid: "39024174"
---
# <a name="creating-the-web-service-proxy"></a>建立 Web 服務 Proxy
  用戶端與 Web 服務可以使用 SOAP 訊息來進行通訊，這會以 XML 來封裝輸入與輸出參數。 Proxy 類別會將參數對應至 XML 元素，然後透過網路傳送 SOAP 訊息。 以此方式，Proxy 類別可讓您免於在 SOAP 層級與 Web 服務通訊，並可讓您在任何支援 SOAP 與 Web 服務 Proxy 的開發環境中，叫用 Web 服務方法。  
  
 有兩種方式可以將 Proxy 類別新增至使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 的開發專案：使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中的 WSDL 工具，以及在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中新增 Web 參考。 下列小節針對這個主題進行更詳細的討論。  
  
## <a name="adding-the-proxy-using-the-wsdl-tool"></a>使用 WSDL 工具加入 Proxy  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 包含 Web 服務描述語言工具 (Wsdl.exe)，這可讓您在 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 開發環境中產生要使用的 Web 服務 Proxy。 使用支援 Web 服務的語言 (目前 C# 與 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) 來建立用戶端 Proxy 的最常見方式是使用 WSDL 工具。  
  
 **使用 Wsdl.exe 將 Proxy 類別新增至專案**  
  
1.  從命令提示，使用 Wsdl.exe 來建立 Proxy 類別，(至少) 將 URL 指定為報表伺服器 Web 服務。  
  
     例如，下列命令提示陳述式會為報表伺服器 Web 服務的管理端點指定 URL：  
  
    ```  
    wsdl /language:CS /n:"Microsoft.SqlServer.ReportingServices2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     WSDL 工具會接受一些命令提示引數以產生 Proxy。 上述範例會指定 C# 語言，這是要在 Proxy 中使用的建議命名空間 (如果使用一個以上的 Web 服務端點，便可防止名稱衝突)，並產生稱為 ReportingService2010.cs 的 C# 檔案。 如果範例已指定 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]，則此範例將會產生名為 ReportingService2010.vb 的 Proxy 檔案。 這個檔案是在您執行命令的目錄中建立。  
  
2.  將 Proxy 類別編譯為組件檔 (使用副檔名 .dll) 並在專案中參考它，或是將類別加入為專案項目。  
  
    > [!NOTE]  
    >  當您手動將 Proxy 類別加入專案，需要將參考加入 System.Web.Services.dll。 如果您在 Visual Studio .NET 中使用 Web 參考加入 Proxy，則會為您自動建立參考。 如需詳細資訊，請參閱本主題稍後的「在 Visual Studio 中使用 Web 參考加入 Proxy」。  
  
     在將 Proxy 類別以項目的方式加入專案之後，相關聯的檔案會出現在 [方案總管] 中。  
  
3.  若要以程式設計的方式呼叫服務，請建立 Proxy 類別的執行個體。  
  
     下列程式碼範例示範在專案中建立 <xref:ReportService2010.ReportingService2010> Proxy 類別之執行個體的語法：  
  
```vb  
Dim service As New ReportingService2010()  
```  
  
```csharp  
ReportingService2010 service = new ReportingService2010();  
  
```  
  
 如需有關 Wsdl.exe 工具 (包括其完整的語法) 的詳細資訊，請參閱 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文件集中的＜Web 服務描述語言工具＞。 如需 Web 服務 Proxy 的完整說明，請參閱 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文件集中的＜建立 XML Web 服務 Proxy＞。  
  
## <a name="adding-the-proxy-using-a-web-reference-in-visual-studio"></a>使用 Visual Studio 中的 Web 參考來加入 Proxy  
 Web 參考可讓專案取用一個或多個 Web 服務。 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 可讓使用者遵循一些簡單的步驟，將 Web 服務參考加入專案中。  
  
 **將 Web 參考新增至專案**  
  
1.  在**方案總管**中，選取將取用 Web 服務的專案。  
  
2.  在 [專案] 功能表上，按一下 [新增 Web 參考]。  
  
     [新增 Web 參考] 對話方塊隨即開啟。  
  
3.  在 [URL] 欄位中，輸入報表伺服器 Web 服務的完整路徑。  
  
     報表伺服器 Web 服務的報表執行端點之簡化的 URL，可能如下所示：  
  
    ```  
    http://<Server Name>/reportserver/reportexecution2005.asmx  
    ```  
  
     這個 URL 包含部署報表伺服器 Web 服務的網域、包含服務的資料夾名稱，以及服務的探索檔名稱。 如需不同 URL 項目的完整描述，請參閱[存取 SOAP API](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)。  
  
     Web 服務提供的方法與屬性之描述會出現在左邊的 [瀏覽器] 窗格中。  
  
    > [!NOTE]  
    >  如需與報表伺服器 Web 服務建立關聯之項目的詳細資訊，請參閱[報表伺服器 Web 服務方法](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)。  
  
4.  請確認您的專案可以使用報表伺服器 Web 服務，而且您有適當的權限可以存取報表伺服器。  
  
5.  在 [Web 參考名稱] 欄位中，輸入在程式碼中將以程式設計方式存取報表伺服器 Web 服務所使用的名稱。  
  
6.  選取 [新增參考] 按鈕，在應用程式中建立對 Web 服務的參考。  
  
     [Web 參考名稱] 欄位中所指定名稱的新參考，將出現於**方案總管**中使用中專案的 [Web 參考] 節點之下。  
  
7.  在**方案總管**中，展開 [Web 參考] 資料夾，以寫下在專案中項目的可用 Web 參考類別之命名空間。  
  
     在將 Web 參考新增專案之後，會在**方案總管**的 [Web 參考] 資料夾的某個資料夾中顯示相關聯的檔案。  
  
 在加入 Web 參考之後，請使用下列語法建立 Proxy 類別的執行個體。  
  
```vb  
Dim rs As New myNamespace.myReferenceName.ReportExecutionService()  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
myNamespace.myReferenceName.ReportExecutionService rs = new myNamespace.myReferenceName.ReportExecutionService();  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl";  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
```  
  
 您也可以將 **using** (在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中為**匯入**) 指示詞新增報表伺服器 Web 服務參考。 如果您使用這個指示詞，就不需要完全符合命名空間的類型。 若要這樣做，請將下列程式碼加入檔案中：  
  
```vb  
Import myNamespace.myReferenceName  
```  
  
```csharp  
using myNamespace.myReferenceName;  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [使用 Web 服務和 .NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [技術參考 &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
