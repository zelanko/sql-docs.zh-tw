---
title: Integration Services 開發人員文件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services, programming
- SSIS, programming
- SQL Server Integration Services, programming
- packages [Integration Services], programming
ms.assetid: 60fe148b-a7c4-4289-ae3e-2e949fc1886c
caps.latest.revision: 76
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 53c86f77f5280e7245f4c5a5ca6c5f694138ed10
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="integration-services-developer-documentation"></a>Integration Services 開發人員文件
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包括完全改寫的物件模型，已透過許多功能增強，這使得擴充封包和設計其程式更輕鬆、更彈性且更強大。 開發人員幾乎可以擴充和程式設計 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的每個層面。  
  
 身為 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 開發人員，有兩種主要的方式可進行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的程式設計：  
  
-   您可以透過撰寫在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中提供的元件，在封裝中提供自訂功能來擴充封包。  
  
-   您可以從自己的應用程式以程式設計方式建立、設定和執行封裝。  
  
 如果您發現 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中的內建元件不符合需求，可以透過編寫自己的延伸模組，擴充 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的功能。 在這種方法中，您有兩個完全不同的選項：  
  
-   對於在單一封裝中的特定使用，您可以在指令碼工作中撰寫程式碼以建立自訂工作，或是在指令碼元件中撰寫程式碼以建立自訂資料流程元件，如此便可將其設定為來源、轉換或是目的地。 這些強大的包裝函數會為您撰寫基礎結構程式碼，而且可讓您專門著重在開發自訂功能，不過，比較不容易在其他地方重複使用。  
  
-   若要在多個封裝中使用，您可以建立自訂 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 延伸模組，例如連接管理員、工作、列舉值、記錄提供者以及資料流程元件。 Managed [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型包含基底類別，可提供起點並使開發自訂延伸模組比以前更容易。  
  
 如果您要動態建立封裝，或是要在開發環境以外的地方管理和執行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝，可以使用程式設計方式操作封裝。 您可以載入、修改和執行現有封裝，或是您可以用程式設計方式完全地建立和執行新封裝。 在這種方法中，您有連續範圍的選項：  
  
-   在不須修改的情況下載入並執行現有的封裝。  
  
-   載入現有的封裝、重新設定 (例如，指定不同的資料來源) 然後加以執行。  
  
-   建立新封裝、加入和設定元件、逐物件和逐屬性地進行變更、儲存，然後加以執行。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 程式設計的這些方法將在本章節中說明並以範例示範。  
  
## <a name="in-this-section"></a>本節內容  
 [Integration Services 程式設計概觀](../integration-services/integration-services-programming-overview.md)  
 說明控制流程和資料流程在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 開發工作中的角色。  
  
 [了解同步和非同步轉換](../integration-services/understanding-synchronous-and-asynchronous-transformations.md)  
 說明同步與非同步輸出之間的重要差別，以及會在資料流程中使用這些輸出的元件。  
  
 [以程式設計方式使用連線管理員](../integration-services/working-with-connection-managers-programmatically.md)  
 列出您可從受控碼中使用的連線管理員，以及當程式碼呼叫 **AcquireConnection** 方法時，連線管理員所傳回的值。  
  
 [使用指令碼擴充套件](../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 說明如何透過使用指令碼工作擴充控制流程，或是如何透過使用指令碼元件擴充資料流程。  
  
 [使用自訂物件擴充封裝](../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 說明如何建立和程式設計自訂工作、資料流程元件以及其他封裝物件，以供在多個封裝中使用。  
  
 [以程式設計方式建置套件](../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 描述如何以程式設計方式建立、設定和儲存 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
 [以程式設計方式執行及管理套件](../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 描述如何以程式設計方式列舉、執行和管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
## <a name="reference"></a>參考  
 [Integration Services 錯誤和訊息參考](../integration-services/integration-services-error-and-message-reference.md)  
 列出預先定義的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤碼，以及其符號名稱與描述。  
  
## <a name="related-sections"></a>相關章節  
 [套件開發的疑難排解工具](../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
 描述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供用以在開發期間疑難排解封裝的功能與工具。  
  
## <a name="external-resources"></a>外部資源  
  
-   位於 www.codeplex.com/MSFTISProdSamples 的 CodePlex 範例：[Integration Services 產品範例](http://go.microsoft.com/fwlink/?LinkID=131204)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
  
  
