---
title: 使用 Reporting Services 安全性原則檔 | Microsoft Docs
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
- code groups [Reporting Services]
- CodeGroup elements
- configuration files [Reporting Services]
- code access security [Reporting Services], security policies
- security policies [Reporting Services]
- security configuration files [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: 2280fff6-3de7-44b1-87da-5db0ec975928
caps.latest.revision: 31
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6cce76e0d7ae2aaec45c851fa0ab7ee4e65dedff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222988"
---
# <a name="using-reporting-services-security-policy-files"></a>使用 Reporting Services 安全性原則檔
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會將元件安全性原則資訊儲存在安裝過程中複製到檔案系統的三個組態檔內。 這些組態檔可能會包含 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中程式碼組件之內部使用和使用者定義安全性原則的組合。 這三個組態檔會對應至 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的三個安全性實體元件：報表伺服器和 Windows 服務、報表管理員 Web 應用程式，以及報表設計師預覽視窗。  
  
> [!NOTE]  
>  報表設計師有兩個預覽模式：當在 **DebugLocal** 模式中啟動報表專案時，會啟動預覽索引標籤與快顯預覽視窗。 [預覽] 索引標籤並非安全性實體元件，而且不會套用安全性原則設定。 預覽視窗是用以模擬報表伺服器功能，因此具有原則組態檔，而且您或系統管理員必須修改該檔案，才能在報表設計師中使用自訂組件和自訂延伸模組。  
  
 這些安全性原則組態檔包含安全性類別資訊、某些預設的具名權限集合，以及 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中組件的程式碼群組。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的原則組態檔與 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中決定與電腦和企業層級原則相關聯之程式碼群組階層和權限集合的 Security.config 檔很相似。 這個檔案的位置是 C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\CONFIG\security.config。  
  
## <a name="policy-files-in-reporting-services"></a>Reporting Services 中的原則檔  
 下表將列出 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的原則組態檔、其位置 (假設是預設安裝)，以及其個別功能。  
  
|[檔案名稱]|位置 (預設安裝)|描述|  
|---------------|---------------------------------------|-----------------|  
|rssrvpolicy.config|C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer|報表伺服器原則組態檔。 一旦報表部署至報表伺服器時，這些安全性原則主要會影響報表運算式和自訂組件。 這個原則檔也會影響部署至報表伺服器的自訂資料、傳遞、轉譯和安全性延伸模組。|  
|rsmgrpolicy.config|C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportManager|報表管理員原則組態檔。 這些安全性原則會影響擴充報表管理員的所有組件。例如，自訂傳遞的訂閱使用者介面延伸模組。|  
|rspreviewpolicy.config|C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies|報表設計師獨立預覽原則組態檔。 這些安全性原則會影響預覽和部署期間用於報表中的自訂組件和報表運算式。 這些原則也會影響部署至報表設計師的自訂延伸模組，例如資料處理延伸模組。|  
  
## <a name="modifying-configuration-files"></a>修改組態檔  
 組態設定會指定為 XML 元素或屬性。 如果您了解 XML 和組態檔，就可以使用文字或程式碼編輯器來修改可由使用者定義的設定。 安全性組態檔包含與 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中原則層級相關聯之程式碼群組階層和權限集合的相關資訊。 建議您先使用 .NET Framework 組態公用程式 (Mscorcfg.msc) 或程式碼存取安全性原則公用程式 (Caspol.exe) 來修改 Security.config 檔中的安全性原則，讓原則變更對應至原則檔的有效 XML 組態元素。 一旦您完成此步驟之後，就可以從 Security.config 剪下新的程式碼群組和權限集合並貼入您要加入程式碼權限之元件的原則檔中。  
  
> [!IMPORTANT]  
>  進行任何變更之前，您應該先備份原則組態檔。  
  
 使用這種方法可達成兩項目的。 首先，它可讓您使用視覺化工具來建立 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的程式碼群組和權限集合。 這比從頭開始撰寫 XML 組態元素更簡單。 其次，它可確保您不會使用格式錯誤的 XML 元素和屬性來損毀安全性原則組態檔。 如需有關程式碼存取安全性原則公用程式的詳細資訊，請參閱 MSDN 上的＜使用 Reporting Services 安全性原則檔＞。  
  
 修改原則組態檔之前，您應該先閱讀本節和相關主題中的所有可用資訊。 修改 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的原則組態可能會對 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 元件執行外部程式碼模組的方式造成重大安全性影響。  
  
## <a name="placement-of-codegroup-elements-for-extensions"></a>延伸模組之 CodeGroup 元素的放置方式  
 CodeGroup 元素在安全性原則檔中的放置方式很重要。 針對您開發的延伸模組和自訂組件，建議您將自訂程式碼群組直接放在 URL 成員資格 "$CodeGen$/*" 的現有項目底下，如下面所示：  
  
```  
<CodeGroup  
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust">  
    <IMembershipCondition   
        class="UrlMembershipCondition"  
        version="1"  
        Url="$CodeGen$/*"  
    />  
</CodeGroup>  
<CodeGroup   
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust"  
    Name="MyCustomCodeGroup"  
    Description="Code group for my custom extension">  
        <IMembershipCondition class="UrlMembershipCondition"  
        version="1"  
        Url="C:\Program Files\Microsoft SQL Server\MSSQL\Reporting Services\ReportServer\bin\MyAssembly.dll"  
        />  
</CodeGroup>  
```  
  
 您可以依次加入其他程式碼群組。  
  
## <a name="see-also"></a>另請參閱  
 [了解安全性原則](understanding-security-policies.md)  
  
  
