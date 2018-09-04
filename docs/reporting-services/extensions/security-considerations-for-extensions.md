---
title: 延伸模組的安全性考量 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], extensions
- extensions [Reporting Services], security
- permissions [Reporting Services], extensions
ms.assetid: 58cbdfeb-1105-4a7d-a3b8-b897ff95f367
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 008695a4157fc51080f344d23399d65130dcbe9c
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43270229"
---
# <a name="security-considerations-for-extensions"></a>延伸模組的安全性考量
  以 Common Language Runtime (CLR) 為目標的每個應用程式，必須和 CLR 安全性系統互動。 當這樣的應用程式執行時，CLR 會自動評估它並給與一組權限。 視應用程式獲得的權限而定，它會繼續執行或是產生安全性例外狀況。 特定報表伺服器之安全性原則組態檔中的本機安全性設定與原則，會定義組件獲得的程式碼權限。  
  
 在要求權限之前，您需要知道延伸模組程式碼計劃使用的資源與保護作業，而且也需要知道哪些權限會保護這些資源與作業。 此外，您必須追蹤延伸模組元件呼叫的任何類別庫方法所存取的任何資源。 如需詳細資訊，請參閱《[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 開發人員指南》中的＜要求權限＞。  
  
 部署到報表伺服器的延伸模組必須以完全信任的方式執行，這表示您的延伸模組必須是授與 **FullTrust** 權限集合之程式碼群組的一部分。 這也表示您的延伸模組可以存取透過 CLR 使用的某些伺服器資源與作業，端視為特定報表驗證的使用者而定。 如需程式碼群組和延伸模組的詳細資訊，請參閱 [Reporting Services 中的程式碼存取安全性](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會為所有其延伸模組強制 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 安全性。  
  
 下列條件適用於在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中部署資料處理、傳遞、轉譯和安全性延伸模組：  
  
-   只有本機管理員有部署延伸模組的權限。  
  
-   只有具有適當讀取/寫入權限的使用者可以變更已擴充的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件之組態檔。  
  
-   只有有權限的使用者才有編輯安全性原則檔案的權限，並且允許延伸模組的程式碼存取安全性。  
  
 如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 程式碼存取安全性的詳細資訊，請參閱[安全開發 &#40;Reporting Services&#41;](../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)。  
  
 如需有關 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 安全性的詳細資訊，請參閱《[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 開發人員指南》中的＜.NET Framework 安全性＞。  
  
## <a name="initialization-of-extension-assemblies"></a>延伸模組組件的初始化  
 當報表伺服器第一次將延伸模組載入記憶體時，這些延伸模組會使用服務帳戶認證，因為某些延伸模組組件需要特定權限才能存取系統資源、讀取組態檔以及載入其他的相依組件。 不過，在載入和初始化組件之後，所有對延伸模組組件後續的呼叫，都會使用目前登入的使用者帳戶之認證。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 延伸模組程式庫](../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
