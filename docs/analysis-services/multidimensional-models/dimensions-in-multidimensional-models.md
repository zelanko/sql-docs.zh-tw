---
title: 多維度模型中的維度 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d87c92cb7be3c11fbce9de0f2731135671c8a216
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178212"
---
# <a name="dimensions-in-multidimensional-models"></a>多維度模型中的維度
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  資料庫維度是相關物件的集合 (稱為屬性)，可用來提供與一或多個 Cube 中的事實資料有關的資訊。 例如，產品維度中的典型屬性可能是產品名稱、產品類別目錄、產品線、產品尺寸和產品價格； 這些物件會繫結到資料來源檢視中一或多個資料表內的一或多個資料行， 依預設，這些屬性可以顯示為屬性階層，而且可用來了解 Cube 中的事實資料。 屬性可以組成使用者自訂階層，在使用者瀏覽 Cube 中的資料時，提供導覽路徑來協助使用者。  
  
 Cube 包含使用者的事實資料分析所根據的所有維度； Cube 中資料庫維度的執行個體稱為 Cube 維度，與 Cube 中的一個或多個量值群組相關。 資料庫維度可在 Cube 中使用多次。 例如，事實資料表可以有多個時間相關的事實，而且可以定義個別 Cube 維度來協助分析每一個時間相關的事實； 但是，只需要存在一個時間相關的資料庫維度，這也表示只需要存在一個時間相關的關聯式資料庫資料表，就可以支援以時間為根據的多個 Cube 維度。  

  
## <a name="defining-dimensions-attributes-and-hierarchies"></a>定義維度、屬性和階層  
 定義資料庫和 Cube 維度、屬性和階層最簡單的方法，就是使用 [Cube 精靈]，在定義 Cube 的同時建立維度。 Cube 精靈會根據精靈在資料來源檢視中找到的維度資料表，或您指定要用於 Cube 的維度資料表，來建立維度。 然後，精靈會建立資料庫維度，並將其加入新的 Cube，以建立 Cube 維度。  
  
 建立 Cube 時，也可以將資料庫中的任何現有維度加入新的 Cube 中。 這些維度可能是先前已經為其他 Cube 定義的維度，或已由維度精靈定義的維度。 定義資料庫維度之後，您可以在維度設計師中修改並設定資料庫維度。 您也可以在 Cube 設計師中自訂有限範圍的 Cube 維度。  
  
> [!NOTE]  
>  此外，您也可以透過使用 XMLA 或分析管理物件 (AMO)，以程式設計方式設計並設定維度、屬性和階層。 如需詳細資訊，請參閱 [Analysis Services 指令碼語言 &#40;ASSL&#41; 參考](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)和[使用分析管理物件 &#40;AMO&#41; 來開發](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)。  
  
## <a name="in-this-section"></a>本節內容  
 下表描述此章節的主題。  
  
 [定義資料庫維度](../../analysis-services/multidimensional-models/define-database-dimensions.md)  
 描述如何使用維度設計師修改及設定資料庫維度。  
  
 [維度屬性內容參考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
 描述如何使用維度設計師來定義、修改及設定資料庫維度屬性。  
  
 [定義屬性關聯性](../../analysis-services/multidimensional-models/attribute-relationships-define.md)  
 描述如何使用維度設計師來定義、修改及設定屬性關聯性。  
  
 [建立使用者定義階層](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
 描述如何使用維度設計師來定義、修改及設定維度屬性的使用者自訂階層。  
  
 [使用商業智慧精靈增強維度](http://msdn.microsoft.com/library/12d995d1-75ca-4890-bf4b-a2656910b8d0)  
 描述如何使用 [商業智慧精靈] 來增強資料庫維度。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的 Cube](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
