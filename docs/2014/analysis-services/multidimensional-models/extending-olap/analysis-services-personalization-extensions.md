---
title: Analysis Services 個人化延伸模組 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 313b1764dfb17c3a8b49fa3ffa139668f9b2b421
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62726114"
---
# <a name="analysis-services-personalization-extensions"></a>Analysis Services 個人化延伸模組
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]個人化延伸模組是實現外掛程式架構之概念的基礎。 在外掛程式架構中，您可以動態開發新的 Cube 物件和功能，並輕鬆地與其他開發人員共用。 因此， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]個人化延伸模組所提供的功能，可讓您達到下列目的：  
  
-   **動態設計和部署**在您設計和部署[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]個人化延伸模組之後，使用者就可以在下一個使用者會話開始時存取物件和功能。  
  
-   **介面獨立性**不論您用來建立[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]個人化延伸模組的介面為何，使用者都可以使用任何介面來存取物件和功能。  
  
-   **會話內容** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]個人化延伸模組在現有的基礎結構中不是永久的物件，而且不需要重新處理 cube。 它們會在使用者連接資料庫時針對使用者來公開及建立，而且在整個使用者工作階段期間都維持可用狀態。  
  
-   **快速散發**與[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]其他軟體發展人員共用個人化延伸模組，而不需要深入瞭解如何找到此延伸功能的詳細規格。  
  
 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 個人化延伸模組有許多用途。 例如，假設貴公司的銷售使用不同的貨幣。 您建立一個導出成員，該成員會使用存取此 Cube 之人員所用的當地貨幣來傳回合併的銷售量。 您會將這個成員建立為個人化延伸模組， 然後您可以將這個導出成員與一組使用者共用。 一旦共用之後，這些使用者就可以在連接伺服器之後立刻存取此導出成員。 即使這些使用者所使用的介面與當初建立此導出成員所用的介面不同，他們還是可以存取。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]個人化延伸模組是對現有 managed 元件架構的簡單且簡潔的修改，而且會[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] <xref:Microsoft.AnalysisServices.AdomdServer>在整個物件模型、多維度運算式（MDX）語法和架構資料列集公開。  
  
## <a name="logical-architecture"></a>邏輯架構  
 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 個人化延伸模組的架構是根據 Managed 組件架構，而且具有以下四個基本元素：  
  
 [PlugInAttribute] 自訂屬性  
 啟動服務時， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]會載入必要的元件，並判斷哪些類別具有<xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute>自訂屬性。  
  
> [!NOTE]  
>  
  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 會使用可描述程式碼及影響執行階段行為的方式來定義自訂屬性。 如需詳細資訊，請參閱 MSDN 上《 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]開發人員指南》中的「[屬性總覽](https://go.microsoft.com/fwlink/?LinkId=82929)」主題。  
  
 對於具有<xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute>自訂屬性的所有類別[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ，會叫用其預設的函式。 在啟動時叫用所有建構函式會提供一個共用位置，可以從這個位置建立新的物件，而且此位置與任何使用者活動都無關。  
  
 除了建立有關撰寫及管理個人化延伸模組之資訊的小型快取之外，此類別建構函式通常還會訂閱 <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> 和 <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing> 事件。 無法訂閱這些事件可能會導致 Common Language Runtime (CLR) 記憶體回收行程不當標記此類別來加以清除。  
  
 工作階段內容  
 如果是根據個人化延伸模組的物件，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會在用戶端工作階段期間建立執行環境，並在此環境中動態建立大多數的物件。 就像其他任何 CLR 組件一樣，這個執行環境也可存取其他函數和預存程序。 當使用者會話結束時， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]會移除動態建立的物件並關閉執行環境。  
  
 事件  
 物件的建立是由工作階段事件 `On-Cube-OpenedCubeOpened` 和 `On-Cube-ClosingCubeClosing` 所觸發。  
  
 用戶端與伺服器之間的通訊是透過特定的事件而產生。 這些事件可讓用戶端了解導致用戶端物件建立的狀況。 用戶端的環境是使用兩組事件所動態建立的：工作階段事件和 Cube 事件。  
  
 工作階段事件與伺服器物件有關聯。 當用戶端登入伺服器時， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]會建立會話並觸發<xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened>事件。 當用戶端在伺服器上結束會話時， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]就會<xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>觸發事件。  
  
 Cube 事件與連接物件有關聯。 連接到 Cube 會觸發 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened> 事件。 關閉與 Cube 的連接 (不論是關閉 Cube 還是切換到不同的 Cube) 會觸發 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing> 事件。  
  
 可追蹤性和錯誤處理  
 所有活動都可以使用 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 來追蹤。 未處理的錯誤會報告到 Windows 事件記錄檔。  
  
 所有物件的撰寫和管理都與這個結構無關，而且只有物件的開發人員才需負責。  
  
## <a name="infrastructure-foundations"></a>基礎結構基準  
 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 個人化延伸模組是根據現有的元件。 下列是提供個人化延伸模組功能的增強與改良摘要。  
  
### <a name="assemblies"></a>組件  
 自訂屬性 <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> 可加入您的自訂組件中，以識別 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 個人化延伸模組類別。  
  
### <a name="changes-to-the-adomdserver-object-model"></a>變更到 AdomdServer 物件模型  
 
  <xref:Microsoft.AnalysisServices.AdomdServer> 物件模型中的以下物件已經過增強或是已加入此模型。  
  
#### <a name="new-adomdconnection-class"></a>新的 AdomdConnection 類別  
 
  <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection> 類別是新的，而且會透過屬性和事件公開幾個個人化延伸模組。  
  
 **屬性**  
  
-   
  <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.SessionID%2A> 是一個唯讀字串值，代表目前連接的工作階段識別碼。  
  
-   
  <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.ClientCulture%2A> 是與目前工作階段有關之用戶端文化特性的唯讀參考。  
  
-   
  <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.User%2A> 是代表目前使用者之識別介面的唯讀參考。  
  
 **事件**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>  
  
#### <a name="new-properties-in-the-context-class"></a>Context 類別中的新屬性  
 
  <xref:Microsoft.AnalysisServices.AdomdServer.Context> 類別有兩個新的屬性：  
  
-   
  <xref:Microsoft.AnalysisServices.AdomdServer.Context.Server%2A> 是新伺服器物件的唯讀參考。  
  
-   
  <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentConnection%2A> 是新 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection> 物件的唯讀參考。  
  
#### <a name="new-server-class"></a>新的 Server 類別  
 
  <xref:Microsoft.AnalysisServices.AdomdServer.Server> 類別是新的，而且會透過類別屬性和事件公開幾個個人化延伸模組。  
  
 **屬性**  
  
-   
  <xref:Microsoft.AnalysisServices.AdomdServer.Server.Name%2A> 是代表伺服器名稱的唯讀字串值。  
  
-   
  <xref:Microsoft.AnalysisServices.AdomdServer.Server.Culture%2A> 是與伺服器有關之全域文化特性的唯讀參考。  
  
 **事件**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>  
  
#### <a name="adomdcommand-class"></a>AdomdCommand 類別  
 
  <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> 類別現在支援下列 MDX 命令：  
  
-   [&#40;MDX&#41;的 CREATE MEMBER 語句](/sql/mdx/mdx-data-definition-create-member)  
  
-   [UPDATE MEMBER 語句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-update-member)  
  
-   [DROP MEMBER 語句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-member)  
  
-   [&#40;MDX&#41;建立 SET 語句](/sql/mdx/mdx-data-definition-create-set)  
  
-   [&#40;MDX&#41;的 DROP SET 語句](/sql/mdx/mdx-data-definition-drop-set)  
  
-   [CREATE KPI 語句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-kpi)  
  
-   [DROP KPI 語句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-kpi)  
  
### <a name="mdx-extensions-and-enhancements"></a>MDX 延伸模組和增強功能  
 CREATE MEMBER 命令可利用 `caption` 屬性、`display_folder` 屬性和 `associated_measure_group` 屬性來增強。  
  
 加入 UPDATE MEMBER 命令可在需要更新而造成解決計算中的優先順序遺失時，可避免重新建立成員。 更新無法變更導出成員的範圍、將導出成員移到另一個父系或定義不同的 `solveorder`。  
  
 CREATE SET 命令可利用 `caption` 屬性、`display_folder` 屬性和新的 `STATIC | DYNAMIC` 關鍵字來增強。 [*靜態*] 表示只有在建立時才會評估集合。 *動態*表示每次在查詢中使用集合時，就會評估集合。 如果省略關鍵字，預設值會是 `STATIC`。  
  
 CREATE KPI 和 DROP KPI 命令會加入到 MDX 語法。 KPI 可以從任何 MDX 指令碼動態建立。  
  
### <a name="schema-rowsets-extensions"></a>結構描述資料列集延伸模組  
 在 [MDSCHEMA_MEMBERS*範圍*] 資料行上加入。 範圍值如下：MDMEMBER_SCOPE_GLOBAL=1、MDMEMBER_SCOPE_SESSION=2。  
  
 在 MDSCHEMA_SETS *set_evaluation_coNtext* ] 資料行上加入。 設定評估內容值，如下所示：MDSET_RESOLUTION_STATIC = 1、MDSET_RESOLUTION_DYNAMIC = 2。  
  
 加入 On MDSCHEMA_KPIS 範圍資料行。 範圍值如下所示：MDKPI_SCOPE_GLOBAL=1、MDKPI_SCOPE_SESSION=2。  
  
  
