---
title: Reporting Services 中的程式碼存取安全性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- code groups [Reporting Services]
- code access security [Reporting Services]
- permission sets [Reporting Services]
- evidence [Reporting Services]
- code access security [Reporting Services], about code access security
- named permission sets [Reporting Services]
ms.assetid: 97480368-1fc3-4c32-b1b0-63edfb54e472
caps.latest.revision: 30
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0a6b82f5b7aae4d92b50334f14d51b0b6d17ac79
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33017365"
---
# <a name="code-access-security-in-reporting-services"></a>Reporting Services 中的程式碼存取安全性
  程式碼存取安全性是以下列核心概念為主：辨識項、程式碼群組與具名使用權限集合。 在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中，報表管理員、報表設計師和報表伺服器元件都各自具有一個原則檔，其中針對自訂組件以及資料、傳遞、轉譯和安全性延伸模組設定了程式碼存取安全性。 下列各節將提供程式碼存取安全性的概觀。 如需本節中涵蓋之主題的詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文件中的＜安全性原則模型＞。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 使用程式碼存取安全性的原因是，雖然報表伺服器是以 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 技術為基礎，但是一般 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 應用程式與報表伺服器之間仍有大幅差異。 一般 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 應用程式不會執行使用者程式碼。 反之，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會使用開放且可延伸的架構，允許使用者使用報表定義語言的 **Code** 項目針對報表定義檔案進行程式設計，以及在自訂組件中開發專用功能，以便用於報表中。 此外，開發人員可以設計和開發功能強大的延伸模組，以便強化報表伺服器的功能。 由於這項強大功能與彈性，因此產生了盡可能提供保護與安全性的需求。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 開發人員可以在報表中使用任何 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 組件，而且能以原生方式呼叫所有部署至全域組件快取之組件的功能。 報表伺服器唯一可控制的事項就是要針對報表運算式和載入的自訂組件提供哪些權限。 在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中，自訂組件預設會收到僅限**執行**的權限。  
  
## <a name="evidence"></a>辨識項  
 辨識項是指 Common Language Runtime (CLR) 用來決定程式碼組件之安全性原則的資訊。 辨識項會向執行階段指出程式碼具有特定特性。 常見的辨識項形式包括數位簽章和組件的位置。 不過，您也可以自行設計辨識項，以便表示對應用程式有意義的其他資訊。  
  
 組件和應用程式網域都是根據辨識項收到權限。 例如，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 嘗試存取之組件的位置是其中一種常見的弱式名稱組件辨識項形式。 這稱為 URL 辨識項。 部署至報表伺服器之自訂資料處理延伸模組的 URL 辨識項可能是 "C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll"。 組件的強式名稱或數位簽章是另一種常見的辨識項形式。 在此情況下，辨識項就是組件的公開金鑰資訊。  
  
## <a name="code-groups"></a>程式碼群組  
 程式碼群組是具有指定成員資格條件的程式碼邏輯群組。 任何符合成員資格條件的程式碼都包含在此群組中。 系統管理員會透過管理程式碼群組及其相關聯的權限集合，設定安全性原則。  
  
 程式碼群組的成員資格條件是以辨識項為基礎。 例如，程式碼群組的 URL 成員資格是以 URL 辨識項為基礎。 Common Language Runtime (CLR) 會使用識別特性 (例如 URL 辨識項) 來描述程式碼以及判斷是否符合群組的成員資格條件。 例如，如果程式碼群組的成員資格條件是「組件中的程式碼 C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll」，執行階段就會檢查辨識項，以便判斷程式碼是否源自該位置。 這種程式碼群組的組態項目範例可能如下所示：  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="FullTrust"  
   Name="MyCodeGroup"  
   Description="Code group for my data processing extension">  
      <IMembershipCondition class="UrlMembershipCondition"  
         version="1"  
         Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll"  
       />  
</CodeGroup>  
```  
  
 您應該與系統管理員或應用程式部署專家一起判斷自訂組件或 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 延伸模組所需的程式碼存取安全性和程式碼群組類型。  
  
## <a name="named-permission-sets"></a>具名使用權限集合  
 具名使用權限集合是指系統管理員可用來與程式碼群組建立關聯的權限集合。 大部分具名使用權限集合都至少包含一個權限、名稱和權限集合的描述。 系統管理員可以使用具名使用權限集合來建立或修改程式碼群組的安全性原則。 相同的具名使用權限集合可以與多個程式碼群組產生關聯。 CLR 提供了一些內建的具名使用權限集合，包括 **Nothing**、**Execution**、**Internet**、**LocalIntranet**、**Everything** 和 **FullTrust**。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的自訂資料、傳遞、轉譯和安全性延伸模組必須在 **FullTrust** 權限集合底下執行。 請與系統管理員一起針對 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 延伸模組加入適當的程式碼群組和成員資格條件。  
  
 您可以將自己使用之自訂組件的自訂權限等級與報表產生關聯。 例如，如果您想要允許組件存取特定檔案，就可以建立具有特定檔案 I/O 存取權的具名使用權限集合，然後將該權限集合指派給程式碼群組。 下列權限集合會授與 MyFile.xml 檔的唯讀存取權：  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="MyNewFilePermissionSet"  
   Description="A special permission set that grants read access to my file.">  
    <IPermission class="FileIOPermission"  
       version="1"  
       Read="C:\MyFile.xml"/>  
    <IPermission class="SecurityPermission"  
       version="1"  
       Flags="Assertion, Execution"/>  
</PermissionSet>  
```  
  
 您授與此權限集合的程式碼群組可能如下所示：  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="MyNewFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\MyCustomAssembly.dll"/>  
</CodeGroup>  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全開發 &#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
