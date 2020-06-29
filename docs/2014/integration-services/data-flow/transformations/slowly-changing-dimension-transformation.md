---
title: 緩時變維度轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.slowlychangingdimtrans.f1
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- SCD transformation
- updating slowly changing dimensions
ms.assetid: f8849151-c171-4725-bd25-f2c33a40f4fe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a609147a58a426ac89708b36d1e098f170c8b530
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430295"
---
# <a name="slowly-changing-dimension-transformation"></a>緩時變維度轉換
  「緩時變維度」轉換可在資料倉儲維度資料表中協調記錄的更新與插入。 例如，您可利用此轉換來設定轉換輸出，該轉換輸出會使用 AdventureWorks OLTP 資料庫中 Production.Products 資料表的資料，在 [!INCLUDE[ssSampleDBDWobject](../../../includes/sssampledbdwobject-md.md)] 資料庫的 DimProduct 資料表內插入和更新記錄。  
  
> [!IMPORTANT]  
>  「緩時變維度精靈」只支援與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的連接。  
  
 「緩時變維度」轉換會提供下列功能，以管理緩時變維度：  
  
-   將傳入資料列與查閱資料表中的資料列比對，以識別新的和現有的資料列。  
  
-   在不允許變更時識別包含變更的傳入資料列。  
  
-   識別需要更新之推斷的成員記錄。  
  
-   識別包含需要插入新記錄和更新過期記錄之記錄變更的傳入資料列。  
  
-   偵測包含需要更新現有記錄 (包括過期記錄) 變更的傳入資料列。  
  
 「緩時變維度」轉換支援四個類型的變更：變更屬性、記錄屬性、固定屬性及推斷的成員。  
  
-   變更屬性變更會覆寫現有記錄。 此種變更相當於「類型 1」變更。 「緩時變維度」轉換會將這些資料列導向稱為 [變更屬性更新輸出]  的輸出。  
  
-   記錄屬性變更會新建記錄，而不是更新現有記錄。 現有記錄中唯一允許的變更，是更新指示記錄為目前記錄還是過期記錄的資料行。 此種變更相當於「類型 2」變更。 「緩時變維度」轉換會將這些資料列導向至兩個輸出：[記錄屬性插入輸出]  及 [新輸出]  。  
  
-   固定屬性變更指示資料行的值不得變更。 「緩時變維度」轉換會偵測變更，並可將具有變更的資料列導向稱為 [固定屬性輸出]  的輸出。  
  
-   推斷的成員指示資料列在維度資料表中為推斷的成員記錄。 當事實資料表參考尚未載入的維度成員時就會有推斷的成員。 會建立最低推斷的成員記錄以預期相關的維度資料，該相關維度資料會在維度資料的後續載入中提供。 「緩時變維度」轉換會將這些資料列導向稱為 [推斷的成員更新]  的輸出。 當載入推斷成員的資料時，可以更新現有的記錄而不是建立新記錄。  
  
> [!NOTE]  
>  「緩時變維度」轉換不支援需要變更維度資料表的「類型 3」變更。 藉由識別具有固定屬性更新類型的資料行，您可以擷取適用「類型 3」變更的資料值。  
  
 在執行階段，「緩時變維度」轉換會首先嘗試將傳入資料列與查閱資料表中的記錄比對。 如果找不到相符部分，則傳入資料列會成為新記錄；因此，「緩時變維度」轉換不會執行其他工作，並會將資料列導向 [新輸出]  。  
  
 如果找到相符部分，「緩時變維度」轉換會偵測資料列是否包含變更。 如果資料列包含變更，則「緩時變維度」轉換會識別每個資料行的更新類型，並將資料列導向 [變更屬性更新輸出]  、[固定屬性輸出]  、[記錄屬性插入輸出]  或 [推斷的成員更新輸出]  。 如果資料列未變更，則「緩時變維度」轉換會將資料列導向 [不變更輸出]  。  
  
## <a name="slowly-changing-dimension-transformation-outputs"></a>緩時變維度轉換輸出  
 「緩時變維度」轉換擁有一個輸入和最多六個輸出。 輸出會將資料列導向至對應到此資料列的更新與插入需求之資料流程子集。 此轉換不支援錯誤輸出。  
  
 下表描述轉換輸出及其後續資料流程的需求。 該需求會描述「緩時變維度精靈」建立的資料流程。  
  
|輸出|描述|資料流程需求|  
|------------|-----------------|----------------------------|  
|**[變更屬性更新輸出]**|會更新查閱資料表中的記錄。 此輸出用於變更屬性資料列。|「OLE DB 命令」轉換會使用 UPDATE 陳述式更新記錄。|  
|**[固定屬性輸出]**|不得變更之資料列中的值與查閱資料表中的值不相符。 此輸出用於固定屬性資料列。|不會建立任何預設資料流程。 如果轉換已設定為遇到固定屬性資料行的變更之後繼續，則應該建立擷取這些資料列的資料流程。|  
|**[記錄屬性插入輸出]**|查閱資料表至少包含一個相符的資料列。 標示為「目前」的資料列現在必須標示為「已過期」。 此輸出用於記錄屬性資料列。|「衍生的資料行」轉換會為過期資料列和目前資料列指標建立資料行。 「OLE DB 命令」轉換會更新現在必須標示為「已過期」的記錄。 具有新資料行值的資料列會導向至「新輸出」，在此會插入該資料列並將其標示為「目前」。|  
|**[推斷的成員更新輸出]**|會插入推斷之維度成員的資料列。 此輸出用於推斷的成員資料列。|「OLE DB 命令」轉換會使用 SQL UPDATE 陳述式更新記錄。|  
|**[新輸出]**|查閱資料表不包含相符的資料列。 會將資料列加入維度資料表。 此輸出用於新資料列和記錄屬性資料列的變更。|「衍生的資料行」轉換會設定目前資料列指標，而 OLE DB 目的地則會插入該資料列。|  
|**[不變更輸出]**|查閱資料表中的值與資料列值相符。 此輸出用於不變更的資料列。|因為「緩時變維度」轉換不執行任何工作，所以不會建立任何預設資料流程。 如果您要擷取這些資料列，則應該為此輸出建立資料流程。|  
  
## <a name="business-keys"></a>商務索引鍵  
 「緩時變維度」轉換至少需要一個商務索引鍵資料行。  
  
 「緩時變維度」轉換不支援 Null 商務索引鍵。 如果資料包含商務索引鍵資料行為 Null 的資料列，則應該從資料流程移除那些資料列。 您可利用「條件式分割」轉換，來篩選商務索引鍵資料行包含 Null 值的資料列。 如需詳細資訊，請參閱 [Conditional Split Transformation](conditional-split-transformation.md)。  
  
## <a name="optimizing-the-performance-of-the-slowly-changing-dimension-transformation"></a>最佳化緩時變維度轉換的效能  
 如需如何改善緩時變維度轉換效能的建議，請參閱 [資料流程效能功能](../data-flow-performance-features.md)。  
  
## <a name="troubleshooting-the-slowly-changing-dimension-transformation"></a>疑難排解緩時變維度轉換  
 您可以記錄緩時變維度轉換對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解緩時變維度轉換對外部資料來源執行的連接、命令和查詢。 若要記錄緩時變維度轉換對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷]  事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-slowly-changing-dimension-transformation"></a>設定緩時變維度轉換  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="configuring-the-slowly-changing-dimension-transformation-outputs"></a>設定緩時變維度轉換輸出  
 在維度資料表中協調記錄的更新與插入是一項複雜的工作，特別是如果同時使用「類型 1」和「類型 2」變更。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師提供兩種方法，以設定緩時變維度的支援：  
  
-   [進階編輯器]  對話方塊，在其中您可以選取連接、設定一般與自訂元件屬性、選擇輸入資料行，以及設定六個輸出上的資料行屬性。 若要完成緩時變維度支援的設定工作，您必須手動建立「緩時變維度」轉換所使用之輸出的資料流程。 如需詳細資訊，請參閱 [資料流程](../data-flow.md)。  
  
-   「載入維度精靈」，其會引導您執行設定「緩時變維度」轉換和建立轉換輸出的資料流程等步驟。 若要變更緩時變維度的組態，請重新執行「載入維度精靈」。 如需詳細資訊，請參閱 [使用緩時變維度精靈來設定輸出](configure-outputs-using-the-slowly-changing-dimension-wizard.md)。  
  
## <a name="related-tasks"></a>相關工作  
 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
  
-   blogs.msdn.com 上的部落格項目 [Optimizing the Slowly Changing Dimension Wizard](https://go.microsoft.com/fwlink/?LinkId=199481)(最佳化緩時變維度精靈)。  
  
  
