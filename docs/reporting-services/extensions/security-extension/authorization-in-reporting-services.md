---
title: Reporting Services 中的授權 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- authorization [Reporting Services]
ms.assetid: 15fc1c7b-560c-4737-b126-e0d428a1b530
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2210d5eb5997ec66e707a90cdc52dc24328e6f6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193346"
---
# <a name="authorization-in-reporting-services"></a>Reporting Services 中的授權
  授權這項程序可決定是否應該將要求的存取權類型授與某個識別，允許其對於報表伺服器資料庫中特定資源進行存取。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 使用以角色為基礎的授權架構，會根據應用程式的使用者角色指派，將使用者存取權授與指定的資源。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的安全性延伸模組包含授權元件的實作，是用以在使用者通過報表伺服器上的驗證之後，授與存取權給他們。 當使用者透過 SOAP API 與透過 URL 存取，嘗試在系統上或是報表伺服器項目執行作業時，就會叫用授權。 這是透過安全性延伸模組介面 **IAuthorizationExtension2** 來達成的。 如前所述，您所部署的任何延伸模組都會自 **IExtension** 繼承基底介面。 **IExtension** 與 **IAuthorizationExtension2** 是 **Microsoft.ReportingServices.Interfaces** 命名空間的成員。  
  
## <a name="checking-access"></a>檢查存取  
 在授權中，任何自訂安全性實作的關鍵在於存取檢查，這個檢查是實作在 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 方法之中。 每次使用者嘗試在報表伺服器上執行作業時，就會呼叫 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>。 每個作業類型都會多載 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 方法。 若是資料夾作業，存取檢查的範例可能如下所示：  
  
```  
// Overload for Folder operations  
public bool CheckAccess(  
   string userName,   
   IntPtr userToken,   
   byte[] secDesc,   
   FolderOperation requiredOperation)  
{  
   // If the user is the administrator, allow unrestricted access.  
   if (userName == m_adminUserName)   
      return true;  
  
   AceCollection acl = DeserializeAcl(secDesc);  
   foreach(AceStruct ace in acl)  
   {  
         if (userName == ace.PrincipalName)  
         {  
            foreach(FolderOperation aclOperation in   
               ace.FolderOperations)  
            {  
               if (aclOperation == requiredOperation)  
                     return true;  
            }  
         }  
   }  
   return false;  
}  
```  
  
 報表伺服器透過傳遞登入使用者的名稱、使用者 Token、項目的安全性描述項，以及要求的作業，來呼叫 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 方法。 在這裡您將檢查使用者名稱的安全性描述項以及適當的權限以完成要求，然後傳回 **true** 以表示授與存取，或是傳回 **false** 來表示存取遭到拒絕。  
  
## <a name="security-descriptors"></a>安全性描述項  
 在報表伺服器資料庫中，設定項目上的授權原則時，用戶端應用程式 (例如報表管理員) 會將使用者資訊連同項目的安全性原則一起提交到安全性延伸模組。 這個安全性原則與使用者資訊統稱為安全性描述項。 安全性描述項在報表伺服器資料庫中包含項目的下列資訊：  
  
-   具有某些類型的權限以執行項目上之作業的群組或是使用者。  
  
-   項目類型。  
  
-   控制項目存取的判別存取控制清單。  
  
 使用 Web 服務 <xref:ReportService2010.ReportingService2010.SetPolicies%2A> 與 <xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A> 方法來建立安全性描述項。  
  
### <a name="authorization-flow"></a>授權流程  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 授權是由目前設定成在伺服器上執行的安全性延伸模組來控制。 授權是以角色為基礎，並受限於 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 安全性架構提供的權限與作業。 下圖描述授權使用者的程序，以便在報表伺服器資料庫中的項目上操作：  
  
 ![Reporting Services 安全性授權流程](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionauthorizationflow.gif "Reporting Services 安全性授權流程")  
  
 如本圖所示，授權會遵循這個順序：  
  
1.  一旦驗證之後，用戶端應用程式會透過 Reporting Services Web 服務方法，來向報表伺服器提出要求。 驗證 Ticket 會以每個 Web 要求的 HTTP 標頭中之 Cookie 形式，傳遞到報表伺服器。  
  
2.  Cookie 會在進行任何存取檢查之前先驗證。  
  
3.  一旦驗證 Cookie 之後，報表伺服器就會呼叫 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> 並提供識別給使用者。  
  
4.  使用者嘗試透過 Reporting Services Web 服務執行作業。  
  
5.  報表伺服器會呼叫 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 方法。  
  
6.  會將安全性描述項擷取和傳遞到 <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> 的自訂安全性延伸模組實作。 此時，會將使用者、群組或是電腦與被存取的項目之安全性描述項進行比較，並授權可執行要求的作業。  
  
7.  如果使用者已獲得授權，則 Web 服務會執行作業，並將回應傳回給呼叫的應用程式。  
  
  
