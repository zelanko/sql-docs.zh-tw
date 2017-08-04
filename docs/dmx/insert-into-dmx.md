---
title: "插入 (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INSERT INTO
- INSERT
- INSERT_INTO
dev_langs:
- DMX
helpviewer_keywords:
- SKIP (DMX)
- mapped model columns element
- source data query element
- <mapped model columns> element
- <source data query> element
- INSERT INTO statement
- mining models [Analysis Services], processing
- training mining models
- mining structures [DMX], processing
ms.assetid: 85eed207-396c-4a95-a74e-2acc1abc7e2c
caps.latest.revision: 49
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eeb42798d1a095ce08a081144d33961c40ee8dd8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  處理指定的資料採礦物件。 如需有關處理採礦模型與採礦結構的詳細資訊，請參閱[處理需求及考量 &#40; 資料採礦 &#41;](../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 如果指定採礦結構，則陳述式會處理採礦結構及其所有相關聯的採礦模型。 如果指定採礦模型，陳述式就只會處理採礦模型。  
  
## <a name="syntax"></a>語法  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>引數  
 *model*  
 模型識別碼。  
  
 *結構*  
 結構識別碼。  
  
 *對應的模型資料行*  
 資料行識別碼與巢狀識別碼的逗號分隔清單。  
  
 *來源資料查詢*  
 提供者自訂格式中的來源查詢。  
  
## <a name="remarks"></a>備註  
 如果您未指定**採礦模型**或**採礦結構**，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]搜尋名稱為基礎的物件類型，並處理正確的物件。 如果伺服器包含具有相同名稱的採礦結構與採礦模型，就會傳回錯誤。  
  
 使用第二種語法形式，INSERT INTO*\<物件 >*。COLUMN_VALUES，您可以將資料直接插入的模型資料行不必定型模型。 這種方法以精簡、已排序的方式提供模型的資料行資料，當您處理包含階層或已排序資料行的資料集時很有用。  
  
 如果您使用**INSERT INTO**與採礦模型或採礦結構，並保持關閉\<對應模型資料行 > 和\<來源資料查詢 > 引數，陳述式的行為類似**ProcessDefault**，使用已存在的繫結。 如果繫結不存在，陳述式就會傳回錯誤。 如需有關**ProcessDefault**，請參閱[處理選項和設定 &#40;Analysis Services &#41;](../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md). 下列範例會顯示語法：  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 如果您指定**採礦模型**並提供處理對應的資料行和來源資料查詢、 模型與相關聯的結構。  
  
 下表會根據物件的狀態，提供不同陳述式格式之結果的描述。  
  
|引數|物件的狀態|結果|  
|---------------|----------------------|------------|  
|INSERT INTO MINING MODEL*\<模型 >*|處理採礦結構。|處理採礦模型。|  
||不處理採礦結構。|處理採礦模型與採礦結構。|  
||採礦結構包含其他的採礦模型。|處理失敗。 您必須重新處理結構與相關聯的採礦模型。|  
|INSERT INTO MINING STRUCTURE*\<結構 >*|處理或不處理採礦結構。|處理採礦結構與相關聯的採礦模型。|  
|INSERT INTO MINING MODEL*\<模型 >* （包含來源查詢）<br /><br /> 或<br /><br /> INSERT INTO MINING STRUCTURE*\<結構 >* （包含來源查詢）|結構或模型早已包含內容。|處理失敗。 您必須先使用執行此作業中，清除物件[DELETE &#40; DMX &#41;](../dmx/delete-dmx.md)。|  
  
## <a name="mapped-model-columns"></a>對應的模型資料行  
 使用\<對應模型資料行 > 項目，您可以在採礦模型中對應資料來源的資料行的資料行。 \<對應模型資料行 > 項目具有下列格式：  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 使用**略過**，您可以排除必須存在於來源查詢、 但沒有採礦模型中的某些資料行。 當您對於輸入資料列集中包含的資料行沒有任何控制權時，SKIP 將會非常實用。 如果您正在撰寫自己的 OPENQUERY，比較好的作法是省略 SELECT 資料行清單中的資料行，而不是使用 SKIP。  
  
 當需要輸入資料列集來執行聯結時，SKIP 也非常實用，但是採礦結構不會使用此資料行。 這個處理的典型範例就是採礦結構及包含巢狀資料表的採礦模型。 此結構的輸入資料列集將會有一個用來透過 SHAPE 子句建立階層式資料列集的外部索引鍵資料行，但是此模型中幾乎都不會使用此外部索引鍵資料行。  
  
 SKIP 的語法要求您在沒有對應採礦結構資料行的輸入資料列集中的個別資料行位置插入 SKIP。 例如，在底下的巢狀資料表範例中，必須在 APPEND 子句中選取 OrderNumber，好讓它可以在 RELATE 子句中用來指定聯結；但是，您不想要將 OrderNumber 資料插入採礦結構的巢狀資料表內。 因此，此範例會在 INSERT INTO 引數中使用 SKIP 關鍵字，而不是 OrderNumber。  
  
## <a name="source-data-query"></a>來源資料查詢  
 \<來源資料查詢 > 元素可以包含下列資料來源類型：  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **圖形**  
  
-   傳回資料列集的任何 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 查詢  
  
 如需有關資料來源類型的詳細資訊，請參閱[&#60; 來源資料查詢 &#62;](../dmx/source-data-query.md)。  
  
## <a name="basic-example"></a>基本範例  
 下列範例會使用**OPENQUERY**來定型貝氏機率分類模型中的目標郵寄資料為基礎[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]資料庫。  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>巢狀資料表範例  
 下列範例會使用**圖形**來定型包含巢狀的資料表的關聯採礦模型。 請注意，第一行包含**略過**改為所需的 OrderNumber **SHAPE_APPEND**陳述式，但不是採礦模型中使用。  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

