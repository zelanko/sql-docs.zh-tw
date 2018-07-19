---
title: Reporting Services 中的驗證 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], authentication
- forms-based authentication [Reporting Services]
- authentication [Reporting Services]
- custom authentication [Reporting Services]
ms.assetid: 103ce1f9-31d8-44bb-b540-2752e4dcf60b
caps.latest.revision: 23
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 18ea77b885dd7aed809eb1ebda04bbfddad11137
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235018"
---
# <a name="authentication-in-reporting-services"></a>Reporting Services 中的驗證
  驗證是建立使用者對識別的權限之程序。 您可以使用許多技術來驗證使用者。 最常見的方式是使用密碼。 例如，當您實作表單驗證時，想要查詢使用者是否有認證 (通常是透過某個介面來要求登入名稱與密碼)，然後針對資料存放區來驗證使用者，例如資料庫資料表或是組態檔。 如果無法驗證認證，驗證程序會失敗，而且使用者將假設匿名識別。  
  
## <a name="custom-authentication-in-reporting-services"></a>Reporting Services 中的自訂驗證  
 在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中，Windows 作業系統會透過整合式安全性，或是透過使用者認證之明確接收與驗證，來處理使用者的驗證。 在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中可以開發自訂驗證，以支援其他的驗證配置。 這是透過安全性延伸介面 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension> 來達成。 所有的延伸模組都會針對報表伺服器所部署和使用的任何延伸模組，自 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 基底介面繼承。 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 以及 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension> 是 <xref:Microsoft.ReportingServices.Interfaces> 命名空間的成員。  
  
 在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中針對報表伺服器驗證的主要方法是 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 方法。 Reporting Services Web 服務的這個成員，可用以將使用者認證傳遞給報告伺服器以供驗證。 您的基礎安全性延伸模組會實作**IAuthenticationExtension.LogonUser**其中包含您的自訂驗證程式碼。 在表單驗證範例中，**LogonUser** 會針對提供的認證以及資料庫中的自訂使用者存放區執行驗證檢查。 **LogonUser** 的實作範例看起來像這樣：  
  
```  
public bool LogonUser(string userName, string password, string authority)  
{  
   return AuthenticationUtilities.VerifyPassword(userName, password);  
}  
  
```  
  
 下列範例函數是用以驗證提供的認證：  
  
```  
  
internal static bool VerifyPassword(string suppliedUserName,  
   string suppliedPassword)  
{   
   bool passwordMatch = false;  
   // Get the salt and pwd from the database based on the user name.  
   // See "How To: Use DPAPI (Machine Store) from ASP.NET," "How To:  
   // Use DPAPI (User Store) from Enterprise Services," and "How To:  
   // Create a DPAPI Library" for more information about how to use  
   // DPAPI to securely store connection strings.  
   SqlConnection conn = new SqlConnection(  
      "Server=localhost;" +   
      "Integrated Security=SSPI;" +  
      "database=UserAccounts");  
   SqlCommand cmd = new SqlCommand("LookupUser", conn);  
   cmd.CommandType = CommandType.StoredProcedure;  
  
   SqlParameter sqlParam = cmd.Parameters.Add("@userName",  
       SqlDbType.VarChar,  
       255);  
   sqlParam.Value = suppliedUserName;  
   try  
   {  
      conn.Open();  
      SqlDataReader reader = cmd.ExecuteReader();  
      reader.Read(); // Advance to the one and only row  
      // Return output parameters from returned data stream  
      string dbPasswordHash = reader.GetString(0);  
      string salt = reader.GetString(1);  
      reader.Close();  
      // Now take the salt and the password entered by the user  
      // and concatenate them together.  
      string passwordAndSalt = String.Concat(suppliedPassword, salt);  
      // Now hash them  
      string hashedPasswordAndSalt =  
         FormsAuthentication.HashPasswordForStoringInConfigFile(  
         passwordAndSalt,  
         "SHA1");  
      // Now verify them. Returns true if they are equal.  
      passwordMatch = hashedPasswordAndSalt.Equals(dbPasswordHash);  
   }  
   catch (Exception ex)  
   {  
       throw new Exception("Exception verifying password. " +  
          ex.Message);  
   }  
   finally  
   {  
       conn.Close();  
   }  
   return passwordMatch;  
}  
```  
  
## <a name="authentication-flow"></a>驗證流程  
 Reporting Services Web 服務提供自訂驗證延伸模組，以允許報表管理員與報表伺服器的表單驗證。  
  
 Reporting Services Web 服務的 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 方法是用以將認證提交到報表伺服器以進行驗證。 Web 服務使用 HTTP 標頭，將驗證 Ticket (又稱為 Cookie) 從伺服器傳遞到用戶端，以驗證登入要求。  
  
 下圖描述當應用程式是使用報表伺服器來部署，而該報表伺服器是設定成使用自訂驗證延伸模組時，在 Web 服務中驗證使用者的方法。  
  
 ![Reporting Services 安全性驗證流程](../../media/rosettasecurityextensionauthenticationflow.gif "Reporting Services 安全性驗證流程")  
  
 如圖 2 所示，驗證程序如下：  
  
1.  用戶端應用程式會呼叫 Web 服務的 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 方法來驗證使用者。  
  
2.  Web 服務會呼叫<xref:ReportService2010.ReportingService2010.LogonUser%2A>方法的安全性延伸模組，具體而言，此類別可實作**IAuthenticationExtension**。  
  
3.  <xref:ReportService2010.ReportingService2010.LogonUser%2A> 的實作會在使用者存放區或是安全性授權中，驗證使用者名稱與密碼。  
  
4.  一旦成功驗證，Web 服務會為工作階段建立 Cookie 並管理它。  
  
5.  Web 服務會將驗證 Ticket 傳回 HTTP 標頭上的呼叫應用程式。  
  
 當 Web 服務透過安全性延伸模組成功地驗證使用者時，它會產生用於後續要求的 Cookie。 在自訂安全性授權中可能無法保存 Cookie，因為報表伺服器並未擁有安全性授權。 Cookie 會從 <xref:ReportService2010.ReportingService2010.LogonUser%2A> Web 服務方法傳回，而且是用於後續的 Web 服務方法呼叫和 URL 存取中。  
  
> [!NOTE]  
>  為了避免在傳輸期間破壞 Cookie，應該使用安全通訊端層 (SSL) 加密，安全地傳輸從 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 傳回的驗證 Cookie。  
  
 當有安裝自訂安全性延伸模組時，如果您透過 URL 來存取報表伺服器，Internet Information Services (IIS) 與 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 會自動管理驗證 Ticket 的傳輸。 如果您透過 SOAP API 存取報表伺服器，Proxy 類別的實作必須包括其他支援，以管理驗證 Ticket。 如需有關使用 SOAP API 以及管理驗證 Ticket 的詳細資訊，請參閱「透過自訂安全性使用 Web 服務」。  
  
## <a name="forms-authentication"></a>表單驗證  
 表單驗證是一種 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 驗證類型，它會將未驗證的使用者導向 HTML 表單。 一旦使用者提供認證，系統會發出包含驗證 Ticket 的 Cookie。 對於之後的要求，系統會先檢查 Cookie 來查看報表伺服器是否已驗證使用者。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 可加以擴充，以便透過 Reporting Services API 使用可用的安全性擴充性介面。 如果您擴充 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 來使用表單驗證，請為所有與報表伺服器的通訊使用安全通訊端層 (SSL)，以防止惡意的使用者存取其他使用者的 Cookie。 SSL 允許用戶端和報表伺服器驗證彼此，並確保沒有其他的電腦可以讀取兩台電腦之間的通訊內容。 所有透過 SSL 連接從用戶端傳送的資料都會經過加密，因此惡意的使用者將無法攔截傳送到報表伺服器的密碼或是資料。  
  
 通常會實作表單驗證以支援 Windows 之外的平台其帳戶和驗證。 對於要求存取報表伺服器的使用者會顯示圖形介面，而且會將提供的認證提交到安全性授權以進行驗證。  
  
 表單驗證需要該人員在場以輸入認證。 對於直接與 Reporting Services Web 服務通訊的自動執行應用程式，必須將表單驗證與自訂驗證配置結合。  
  
 在下列情況下，表單驗證適用於 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]：  
  
-   您需要儲存和驗證沒有 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帳戶的使用者，而且  
  
-   您需要提供自己的使用者介面表單，做為網站上兩個不同網頁之間的登入網頁。  
  
 撰寫可支援表單驗證的自訂安全性延伸模組時，請考慮下列項目：  
  
-   如果您使用表單驗證，必須在 Internet Information Services (IIS) 中的報表伺服器虛擬目錄上啟用匿名存取。  
  
-   [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 驗證必須設定為 Forms。 您為報表伺服器在 Web.config 檔案中設定 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 驗證。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 可以使用 Windows 驗證或是自訂驗證，來驗證和授權使用者，但並不能同時使用這兩者。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 並不支援同時使用多個安全性延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [實作安全性延伸模組](../security-extension/implementing-a-security-extension.md)  
  
  
