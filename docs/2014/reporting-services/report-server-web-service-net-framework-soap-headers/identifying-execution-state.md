---
title: 識別執行狀態 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- session states [Reporting Services]
- lifetimes [Reporting Services]
- sessions [Reporting Services]
- SessionHeader SOAP header
ms.assetid: d8143a4b-08a1-4c38-9d00-8e50818ee380
caps.latest.revision: 45
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 826e6feb86dec026d22bdfb255361bbbbcd93480
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036957"
---
# <a name="identifying-execution-state"></a>識別執行狀態
  超文字傳輸協定 (HTTP) 是一種無連接且沒有狀態 (Stateless) 的通訊協定，也就是說它不會自動指出不同的要求是否全都來自相同的用戶端，也不會自動指出某個特定瀏覽器執行個體是否仍在主動檢視網頁或網站。 工作階段會建立邏輯連接以透過 HTTP 維護伺服器與用戶端之間的狀態。 與特定工作階段相關的使用者特定資訊又稱為工作階段狀態。  
  
 工作階段管理需要將 HTTP 要求與從相同工作階段產生的其他舊要求相互關聯。 若沒有工作階段管理，由於 HTTP 通訊協定的無連接與無狀態的本質，這些要求會顯得與報表伺服器 Web 服務不相關。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 並不會公開工作階段狀態的整體概念，例如由 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 所公開。 不過，當執行報表時，報表伺服器會以**執行**的形式在方法呼叫之間維護狀態。 執行可讓使用者以數種方式和報表互動，包括從報表伺服器載入報表、設定報表的認證與參數，以及轉譯報表。  
  
 在與報表伺服器進行通訊時，用戶端會使用執行來管理報表檢視以及對報表中其他頁面的使用者導覽，並顯示或是隱藏報表的區段。 用戶端應用程式正在執行的每個報表，會有唯一的執行。  
  
 一般而言，當使用者導覽至瀏覽器或是用戶端應用程式，並選取要檢視的報表時，執行的存留期間會開始。 在已經收到對執行的上一個要求之後，將會在簡短的逾時期間之後捨棄執行 (預設逾時是 20 分鐘)。  
  
 從 Web 服務觀點來看，當呼叫報表伺服器 Web 服務 <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A>, <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A> 或是 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法時，存留期間即開始。 應用程式可以使用其他方法來操作使用中執行 (例如，設定參數和設定資料來源)。 在已經收到對執行的上一個要求之後，將會在簡短的逾時期間之後捨棄執行 (預設逾時是 20 分鐘)。  
  
 應用程式會儲存 <xref:ReportExecution2005.ReportExecutionService.Render%2A>，以便從 <xref:ReportExecution2005.ReportExecutionService.RenderStream%2A> 與 <xref:ReportExecution2005.ExecutionHeader.ExecutionID%2A> 方法在 SOAP 標頭中傳回，來對 Web 服務 <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A> 和 <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A> 方法之間的呼叫持續追蹤多個使用中執行。  
  
 下圖顯示報表的處理和轉譯路徑。  
  
 ![報表處理/轉譯路徑](../../../2014/reporting-services/media/rs-render-process-diagram.gif "報表處理/轉譯路徑")  
  
 為了支援上述功能，已將目前的 SOAP Render 方法分成多個方法，以包含執行初始化、處理和轉譯階段。  
  
 若要以程式設計的方式轉譯報表，您必須：  
  
-   使用 <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A> or <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A> 來載入報表或是報表定義。  
  
-   查看報表是否需要認證或是參數，方法是檢查由 <xref:ReportExecution2005.ExecutionInfo.CredentialsRequired%2A> 或 <xref:ReportExecution2005.ExecutionInfo.ParametersRequired%2A> 傳回的 <xref:ReportExecution2005.ExecutionInfo> 物件之 <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A> 與 <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A> 屬性。  
  
-   若有需要，請使用 <xref:ReportExecution2005.ReportExecutionService.SetExecutionCredentials%2A> 與 <xref:ReportExecution2005.ReportExecutionService.SetExecutionParameters%2A> 方法來設定認證和/或參數。  
  
-   呼叫 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法以轉譯報表。  
  
 當報表是在工作階段中時，儲存在報表伺服器資料庫中的基礎報表有可能會變更。 例如，報表定義有可能會變更，報表有可能會刪除或是移動，而且使用者權限也可能會變更。 如果報表是在使用中工作階段，它不會受到對基礎報表變更的影響 (也就是說，報表會儲存在報表伺服器資料庫中)。  
  
 您也可以使用 URL 存取命令來管理報表工作階段。  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [技術參考 &#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)   
 [使用 Reporting Services SOAP 標頭](../report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)  
  
  