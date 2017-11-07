---
title: "動作 (Analysis Services-多維度資料) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- actions [Analysis Services]
- actions [Analysis Services], about actions
- MDX [Analysis Services], actions
- cubes [Analysis Services], actions
- OLAP objects [Analysis Services], actions
ms.assetid: 07229bb2-805c-427e-8455-69c9ca5d01e0
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a61563367d64f9122441991d125cf987f6ddc4d6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="actions-analysis-services---multidimensional-data"></a>動作 (Analysis Services - 多維度資料)
  動作可以屬於不同類型，而且必須據此來建立。 動作可以是：  
  
-   鑽研動作，該動作會傳回一組資料列，這些資料列表示動作發生所在之 Cube 中選定資料格的基礎資料。  
  
-   報表動作，該動作會從與動作發生所在之 Cube 中選定區段有關的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 內傳回報表。  
  
-   標準動作，該動作會傳回與動作發生所在之 Cube 中選定區段有關的動作元素 (URL、HTML、DataSet、RowSet 和其他元素)。  
  
 查詢介面 (如 ADOMD.NET) 是由用戶端應用程式用來擷取動作，並對使用者公開動作。 如需詳細資訊，請參閱 [使用 ADOMD.NET 來開發](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
 簡單的 <xref:Microsoft.AnalysisServices.Action> 物件是由基本資訊、動作要發生的目標、限制動作範圍的條件以及類型所組成。 基本資訊包括動作的名稱、動作的描述、動作的建議標題和其他內容。  
  
 目標是指動作要發生在 Cube 中的實際位置。 目標是由目標類型和目標物件所組成。 目標類型表示 Cube 中 (啟用動作的地方) 的物件種類。 目標類型可以是層級成員、資料格、階層、階層成員或其他內容。 目標物件是此目標類型的特定物件；如果目標類型為階層，則目標物件會是 Cube 中任何一個定義的階層。  
  
 條件是指在動作事件上評估的 **Boolean** MDX 運算式。 如果條件評估為 **true**，就會執行此動作。 否則，不會執行此動作。  
  
 類型是指要執行之動作的種類。 <xref:Microsoft.AnalysisServices.Action> 是抽象類別，因此使用它時，必須使用任何一個衍生類別。 預先定義的動作有兩種：鑽研和報表。 它們具有相對應的衍生類別： <xref:Microsoft.AnalysisServices.DrillThroughAction> 和 <xref:Microsoft.AnalysisServices.ReportAction>。 其他動作已涵蓋在 <xref:Microsoft.AnalysisServices.StandardAction> 類別中。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，動作是預存的 MDX 陳述式，可呈現給用戶端應用程式並供其使用。 換句話說，動作是定義及儲存在伺服器上的用戶端命令。 動作所包含的資訊還包含指定用戶端應用程式應顯示和處理 MDX 陳述式的時間和方式。 將動作中的資訊當成參數，動作所指定的作業即可啟動應用程式，或可根據動作所提供的準則來擷取資訊。  
  
 動作可讓商務使用者對其分析結果作出反應。 透過儲存並重複使用動作，使用者即可超越傳統分析 (一般是以呈現資料為結束)，並對已探索到的問題和缺點起始方案，因而擴充商業智慧應用程式使其超越 Cube 的範圍。 動作可將用戶端應用程式從複雜的資料轉譯工具轉換為企業作業系統的必要部分。 因為不是專注於傳送資料作為作業應用程式的輸入，所以使用者可在決策過程中「關閉迴圈」。 這個將分析資料轉換成決策的能力對成功的商業智慧應用程式而言十分重要。  
  
 例如，瀏覽 Cube 的商務使用者注意到某產品的目前存貨少。 用戶端應用程式會將一份擷取自 Analysis Services 資料庫的動作清單 (這些動作全部都與低產品存貨值相關) 提供給商務使用者，而商務使用者會針對代表產品之 Cube 成員選取 Order 動作。 然後，Order 動作會在作業資料庫中呼叫預存程序，以起始新的訂單。 這個預存程序會產生適當的資訊，以傳送至訂單輸入系統。  
  
 建立動作時，您可以運用彈性：例如，動作可啟動應用程式，或擷取資料庫中的資訊。 您幾乎可設定從 Cube 的任何部分 (包含維度、層級、成員和資料格) 觸發動作，或為 Cube 的相同部分建立多個動作。 您可以將字串參數傳遞給已啟動的應用程式，並指定動作執行時對使用者所顯示的標題。  
  
> [!IMPORTANT]  
>  為了讓商務使用者使用動作，商務使用者所運用的用戶端應用程式必須支援動作。  
  
## <a name="types-of-actions"></a>動作的類型  
 下表列出 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中所含的動作類型：  
  
|動作類型|說明|  
|-----------------|-----------------|  
|CommandLine|在命令提示字元執行命令。|  
|資料集|將資料集傳回用戶端應用程式。|  
|鑽研|將 drillthrough 陳述式當做運算式傳回，用戶端會執行這個運算式來傳回資料列集。|  
|HTML|在網際網路瀏覽器中執行 HTML 指令碼。|  
|專屬|使用不同於此資料表列出的介面來執行作業。|  
|報表|將一個以 URL 為基礎的參數化要求，提交給報表伺服器，然後將報表傳回用戶端應用程式。|  
|資料列集|將資料列集傳回用戶端應用程式。|  
|Statement|執行 OLE DB 命令。|  
|URL|在網際網路瀏覽器中顯示動態網頁。|  
  
## <a name="resolving-and-executing-actions"></a>解析及執行動作  
 商務使用者存取定義其命令物件的物件時，雖然會自動解析與該動作相關的陳述式，讓用戶端應用程式可使用該陳述式，但是不會自動執行該動作。 只有當商務使用者執行起始動作的用戶端特定作業時，才會執行該動作。 例如，在商務使用者以滑鼠右鍵按一下特定成員或資料格時，用戶端應用程式可能會以快顯功能表形式來顯示動作清單。  
  
## <a name="see-also"></a>請參閱＜  
 [多維度模型中的動作](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
  
  

