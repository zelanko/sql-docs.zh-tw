---
title: 實體架構 (Analysis Services-資料採礦) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- server architecture [Analysis Services]
- architecture [Analysis Services]
ms.assetid: 25eeecf0-6e85-4527-b94d-5503d27edaed
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a147330733efe641b8baf844723e4027e7ada5bc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094148"
---
# <a name="physical-architecture-analysis-services---data-mining"></a>實體架構 (Analysis Services – 資料採礦)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用伺服器和用戶端元件，為商業智慧應用程式提供資料採礦功能：  
  
-   伺服器元件是以 Microsoft Windows 服務的形式實作。 同一部電腦上可以有多個執行個體，每個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體都實作為個別的 Windows 服務執行個體。  
  
-   用戶端使用公用標準 XML for Analysis (XMLA) 與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 通訊；而 XMLA 是一種用於發出命令和接收回應的 SOAP 型通訊協定，並以 Web 服務的形式公開。 用戶端物件模型也可透過 XMLA 予以提供，且可使用 Managed 提供者 (例如 ADOMD.Net) 或原生 OLE DB 提供者進行存取。  
  
-   可以使用資料採礦延伸模組 (DMX，一種資料採礦導向的業界標準查詢語言) 發出查詢命令。 也可以使用 Analysis Services 指令碼語言 (ASSL) 來管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫物件。  
  
## <a name="architectural-diagram"></a>架構圖表  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會當做獨立服務來執行，並與透過 XML for Analysis (XMLA) 所進行的服務通訊 (使用 HTTP 或 TCP)。  
  
 AMO 是介於使用者應用程式與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之間的一層，該執行個體會提供對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理物件的存取權。 AMO 是一個類別庫，它會接收來自用戶端應用程式的命令，並將這些命令轉換成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的 XMLA 訊息。 AMO 會使用執行命令的方法成員以及為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件保存資料的屬性成員，將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體物件當做類別呈現給使用者應用程式。  
  
 下圖顯示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 元件架構，其中包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體內的服務以及與此執行個體互動的使用者元件。  
  
 下圖顯示存取此執行個體的唯一方法就是使用 XML for Analysis (XMLA) 接聽程式 (利用 HTTP 或 TCP)。  
  
> [!WARNING]  
>  DSO 已被取代。 您不應該使用 DSO 來開發方案。  
  
 ![Analysis Services 系統架構圖表](../dev-guide/media/analysisservicessystemarchitecture.gif "Analysis Services 系統架構圖表")  
  
## <a name="server-configuration"></a>伺服器組態  
 一個伺服器執行個體可以支援多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，而且每個資料庫都有自己的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務執行個體，可回應用戶端要求並處理物件。  
  
 如果您想要處理表格式模型和資料採礦及/或多維度模型，則必須安裝個別的執行個體。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援並存安裝表格式模式下所執行的執行個體 (該執行個體會使用 xVelocity 記憶體內部分析引擎 (VertiPaq) 儲存引擎) 以及使用其中一個傳統 OLAP、MOLAP 或 ROLAP 組態所執行的執行個體。 如需詳細資訊，請參閱 [判斷 Analysis Services 執行個體的伺服器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
 用戶端與 Analysis Services 伺服器之間的所有通訊都會使用 XMLA，這是一種與平台和語言無關的通訊協定。 從用戶端收到要求時，Analysis Services 就會判斷此要求是否與 OLAP 或資料採礦有關，然後適當地路由傳送此要求。 如需詳細資訊，請參閱 [OLAP 引擎伺服器元件](../multidimensional-models/olap-physical/olap-engine-server-components.md)。  
  
## <a name="see-also"></a>另請參閱  
 [邏輯架構&#40;Analysis Services-資料採礦&#41;](logical-architecture-analysis-services-data-mining.md)  
  
  
