---
description: StructureColumn (DMX)
title: StructureColumn (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 43e02efd8594497ad4f3c02679a475531489141c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500759"
---
# <a name="structurecolumn-dmx"></a>StructureColumn (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  傳回對應到指定之案例的結構資料行值，或是指定之案例內巢狀資料表的資料表值。  
  
## <a name="syntax"></a>語法  
  
```  
  
StructureColumn('structure column name')  
```  
  
## <a name="arguments"></a>引數  
 structure-column-name。  
 案例或巢狀資料表採礦結構資料行的名稱。  
  
## <a name="result-type"></a>結果類型  
 傳回的類型取決於參數中所參考的資料行類型 \<structure column name> 。 例如，如果所參考的採礦結構資料行包含純量值，此函數會傳回純量值。  
  
 如果所參考的採礦結構資料行是巢狀資料表，此函數會傳回資料表值。 傳回的資料表值可用於子 SELECT 陳述式的 FROM 子句中。  
  
## <a name="remarks"></a>備註  
 此函數為多型，而且可用於允許運算式之陳述式內的任何地方，包括 SELECT 運算式清單、WHERE 條件運算式及 ORDER BY 運算式。  
  
 在「採礦結構」中，資料行的名稱是字串值，因此必須以單引號括住：例如，資料 `StructureColumn('` **行 1** `')` 。 如果有多個資料行同名，則會在括住 SELECT 陳述式的內容中解析名稱。  
  
 使用 **StructureColumn** 函數從查詢傳回的結果會受到模型上任何篩選準則的影響。 也就是說，模型篩選會控制採礦模型內所包含的案例。 因此，結構資料行上的查詢只能傳回採礦模型內使用的案例。 請參閱本主題的「範例」一節，以取得可顯示採礦模型篩選對案例資料表和巢狀資料表之影響的程式碼範例。  
  
 如需有關如何在 DMX SELECT 語句中使用這個函數的詳細資訊，請參閱 [從 &#60;模型&#62; 選取。&#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md) 的案例 [，或從 &#60;結構&#62; 進行選取。案例](../dmx/select-from-structure-cases.md)。  
  
## <a name="error-messages"></a>錯誤訊息  
 如果使用者沒有父採礦結構的鑽研權限，就會引發下列安全性錯誤：  
  
 '% {User/} ' 使用者沒有許可權可向下切入至 '% {model/} ' 採礦模型的父代採礦結構。  
  
 如果指定了無效的結構資料行名稱，就會引發下列錯誤訊息：  
  
 在目前內容 (行% {line/}，資料行% {column/} ) 的 '% {structure/} ' 父代自結構中找不到 '% {structure-column-name/} ' 採礦結構資料行。  
  
## <a name="examples"></a>範例  
 我們將會針對這些範例使用以下採礦結構。 請注意，此採礦結構包含兩個巢狀資料表資料行 `Products` 和 `Hobbies`。 `Hobbies` 資料行中的巢狀資料表具有單一資料行，該資料行會當做巢狀資料表的索引鍵。 `Products` 資料行中的巢狀資料表是一個複雜巢狀資料表，它具有索引鍵資料行及用於輸入的其他資料行。 下列範例說明如何設計資料採礦結構來包含許多不同的資料行 (雖然模型可能不會使用每一個資料行)。 雖然某些資料行在模型層級上對於模式的一般化可能沒有什麼幫助，但是對於鑽研可能會很有幫助。  
  
```  
CREATE MINING STRUCTURE [MyStructure]   
(  
CustomerName TEXT KEY,  
Occupation TEXT DISCRETE,  
Age LONG CONTINUOUS,  
MaritalStatus TEXT DISCRETE,  
Income LONG CONTINUOUS,  
Products  TABLE  
 (  
    ProductNameTEXT KEY,  
    Quantity LONG CONTINUOUS,  
    OnSale BOOLEAN  DISCRETE  
)  
 Hobbies  TABLE  
 (  
    Hobby KEY  
 ))  
```  
  
 接下來，請使用下列範例程式碼，根據您剛才建立的結構建立採礦模型：  
  
```  
ALTER MINING STRUCTURE [MyStructure] ADD MINING MODEL [MyModel] (  
CustomerName,  
Age,  
MaritalStatus,  
Income PREDICT,  
Products   
(  
ProductName  
) WITH FILTER(NOT OnSale)  
) USING Microsoft_Decision_Trees   
WITH FILTER(EXISTS (Products))  
```  
  
### <a name="sample-query-1-returning-a-column-from-the-mining-structure"></a>範例查詢 1：從採礦結構傳回資料行  
 下列範例查詢會傳回定義為採礦模型之一部分的資料行 `CustomerName` 和 `Age`。 但是，此查詢也會傳回 `Age` 資料行 (該資料行是結構的一部分，但不是採礦模型的一部分)。  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation') FROM MyModel.CASES   
WHERE Age > 30  
```  
  
 請注意，篩選資料列來將案例限制為 30 歲以上的客戶會在模型的層級上發生。 因此，此運算式將不會傳回結構資料內所包含但不會由模型所使用的案例。 因為用來建立模型的篩選條件 (`EXISTS (Products)`) 會將案例限制為已購買產品的客戶，此結構內可能會有案例不是由這個查詢所傳回。  
  
### <a name="sample-query-2-applying-a-filter-to-the-structure-column"></a>範例查詢 2：將篩選套用到結構資料行  
 下列範例查詢不但會傳回模型資料行 `CustomerName` 和 `Age` 及巢狀資料表 `Products`，也會傳回巢狀資料表內資料行 `Quantity` 的值 (不屬於此模型的一部分)。  
  
```  
SELECT CustomerName, Age,  
(SELECT ProductName, StructureColumn('Quantity') FROM Products) FROM MA.CASES   
WHERE StructureColumn('Occupation') = 'Architect'  
```  
  
 請注意，在此範例中，篩選準則會套用到結構資料行，以將案例限制為其職業為「架構設計師」 () 的客戶 `WHERE StructureColumn('Occupation') = 'Architect'` 。 因為在建立模型時，模型篩選條件一定會套用到案例中，所以只有在 `Products` 資料表內至少包含一個限定資料列的案例才會包含在模型案例中。 因此，巢狀資料表 `Products` 的篩選及案例 `('Occupation')` 的篩選都會套用。  
  
### <a name="sample-query-3-selecting-columns-from-a-nested-table"></a>範例查詢 3：從巢狀資料表選取資料行  
 下列範例查詢會傳回當做模型中之定型案例使用的客戶名稱。 對於每一位客戶而言，此查詢也會傳回包含購買詳細資料的巢狀資料表。 雖然模型包含資料 `ProductName` 行，但模型不會使用資料行的值 `ProductName` 。 此模型只會檢查產品是否以一般 (`NOT``OnSale`) 價格購買。 此查詢不但會傳回產品名稱，也會傳回所購買的數量 (此模型中未包含數量)。  
  
```  
SELECT CustomerName,    
(SELECT ProductName, StructureColumn('Quantity')FROM Products)   
FROM MyModel.CASES  
```  
  
 請注意，除非採礦模型上已啟用鑽研，否則您無法傳回 `ProductName` 資料行或 `Quantity` 資料行。  
  
### <a name="sample-query-4-filtering-on-and-returning-nested-table-columns"></a>範例查詢 4：篩選及傳回巢狀資料表資料行  
 下列範例查詢會傳回採礦結構中所包含，但是模型中所不包含的案例和巢狀資料表資料行。 此模型已經篩選 `OnSale` 產品，但是此查詢會在採礦結構資料行 `Quantity` 上加入篩選：  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation'),   
(SELECT ProductName, StructureColumn('Quantity') FROM Products)   
FROM MyModel.CASES   
WHERE EXISTS (SELECT * FROM Products WHERE StructureColumn('Quantity')>1)  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)  
  
  
