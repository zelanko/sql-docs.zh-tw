---
title: "了解安全性原則 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- code groups [Reporting Services]
- code access security [Reporting Services], security policies
- Execution permission set
- custom assemblies [Reporting Services], security
- permission sets [Reporting Services]
- expressions [Reporting Services], security
- evidence [Reporting Services]
- FullTrust permission set
- security policies [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: a9bf043a-139a-4929-9a58-244815323df0
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4cb028a3034ddd4dbee5ee3d1b10f696bbe995f3
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="understanding-security-policies"></a>了解安全性原則
  報表伺服器所執行的任何程式碼都必須屬於特定程式碼存取安全性原則的一部分。 這些安全性原則包含將辨識項對應至一組具名使用權限集合的程式碼群組。 通常，程式碼群組會與為該群組中程式碼指定允許權限的具名使用權限集合產生關聯。 執行階段會使用受信任主應用程式或載入程式所提供的辨識項來決定程式碼所屬的程式碼群組，以及因此授與程式碼的權限。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]符合安全性原則架構所定義的[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]通用語言執行平台 (CLR)。 下列各節將描述 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的各種程式碼類型以及與它們相關聯的原則規則。  
  
## <a name="report-server-assemblies"></a>報表伺服器組件  
 報表伺服器組件是包含屬於 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 產品一部分之程式碼的組件。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 是使用 Managed 程式碼組件撰寫而成。所有這些組件都是強式名稱 (亦即，經過數位簽署)。 這些組件的程式碼群組會定義使用**StrongNameMembershipCondition**，這樣會提供辨識項的組件的強式名稱公開金鑰資訊為基礎。 程式碼群組授與**FullTrust**權限集合。  
  
## <a name="report-server-extensions-rendering-data-delivery-and-security"></a>報表伺服器延伸模組 (轉譯、資料、傳遞和安全性)  
 報表伺服器延伸模組是指您或其他協力廠商為了擴充 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 功能而建立的自訂資料、傳遞、轉譯和安全性延伸模組。 您必須授與**FullTrust**這些延伸模組或組件的原則組態檔中的程式碼相關聯[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]所擴充的元件。 擴充功能隨附的[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]會使用報表伺服器公開金鑰簽署並接收**FullTrust**權限集合。  
  
> [!IMPORTANT]  
>  您必須修改[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]原則組態檔，以允許**FullTrust**任何第三方擴充功能。 如果您沒有新增的程式碼群組**FullTrust**的自訂擴充功能，無法用在報表伺服器。  
  
 如需有關原則組態檔中[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]，請參閱[使用 Reporting Services Security Policy Files](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)。  
  
## <a name="expressions-used-in-reports"></a>在報表中使用的運算式  
 報表運算式為內嵌程式碼運算式或使用者定義的方法，內含**程式碼**報表定義語言檔案項目。 沒有程式碼群組已設定原則檔中，授與這些運算式**執行**預設設定的權限。 此程式碼群組如下所示：  
  
```  
<CodeGroup  
   class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="Execution"  
   Name="Report_Expressions_Default_Permissions"  
   Description="This code group grants default permissions for code in report expressions and Code element. ">  
    <IMembershipCondition  
       class="StrongNameMembershipCondition"  
       version="1"  
       PublicKeyBlob="002400..."  
    />  
</CodeGroup>  
```  
  
 **執行**權限可讓程式碼執行 （執行），但若要使用受保護的資源。 在報表內發現的所有運算式都會編譯成一個組件 (稱為「運算式主機」組件)，而該組件會儲存成已編譯報表的一部分。 執行此報表時，報表伺服器會載入運算式主機組件並呼叫該組件以執行運算式。 運算式主機組件會以用來定義所有運算式主機之程式碼群組的特定金鑰進行簽署。  
  
 報表運算式會參考報表物件模型集合 (欄位、參數等等)，然後執行簡單的工作 (例如算術和字串作業)。 執行這些簡單作業的程式碼只需要**執行**權限。 根據預設，使用者定義的方法，在**程式碼**元素以及任何自訂組件授與**執行**中的權限[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]。 因此，對於大部分運算式而言，目前的組態不需要您修改任何安全性原則檔案。 若要將其他權限授與運算式主機組件，系統管理員必須修改報表伺服器和報表設計師的原則組態檔，以及變更報表運算式程式碼群組。 由於它是全域設定，所以變更運算式主機的預設權限就會影響所有報表。 因此，強烈建議您將需要其他安全性的所有程式碼都放入自訂組件中。 如此一來，只有這個組件會被授與您所需的權限。  
  
> [!IMPORTANT]  
>  呼叫外部組件或受保護資源的程式碼應該併入自訂組件中，以便用於報表內。 這樣做可讓您更有效地控制程式碼所要求和判斷提示的權限。 您不應該對進行中的安全方法的呼叫**程式碼**項目。 如此一來您必須授與**FullTrust**報表運算式主機並授與完整的所有自訂程式碼存取 CLR。  
  
> [!CAUTION]  
>  請勿授與**FullTrust**報表運算式主機的程式碼群組。 如果您這樣做，就會讓所有報表運算式進行受保護的系統呼叫。  
  
## <a name="custom-assemblies-referenced-in-reports"></a>在報表中參考的自訂組件  
 某些報表運算式可以呼叫協力廠商程式碼組件 (在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中也稱為自訂組件)。 報表伺服器必須要有至少具有這些組件**執行**原則組態檔中的權限。 根據預設，原則檔案隨附[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]授與**執行**從 「 我的電腦 」 區域開始的所有組件的權限。 您可以視需要將其他權限授與自訂組件。  
  
 在某些情況下，您可能必須執行在報表運算式中需要特定程式碼權限的作業。 一般而言，這表示報表運算式需要呼叫安全的 CLR 程式庫方法 (例如，存取檔案或系統登錄的方法)。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 文件集描述了進行此安全呼叫所需的程式碼權限。若要執行此呼叫，呼叫的程式碼必須被授與這些特定且安全的權限。 若要從報表運算式呼叫或**程式碼**元素，運算式主機組件必須被授與適當的權限。 不過，一旦您將這些權限授與運算式主機，在任何報表之任何運算式中執行的所有程式碼現在都會被授與該特定權限。 從自訂組件進行呼叫以及將特定權限授與該自訂組件是比較安全的做法。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的程式碼存取安全性](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)   
 [安全開發 &#40;Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
