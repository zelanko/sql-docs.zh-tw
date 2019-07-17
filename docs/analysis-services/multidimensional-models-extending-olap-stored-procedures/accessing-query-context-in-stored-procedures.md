---
title: 存取查詢內容中的預存程序 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1679b5ddaf2c3abefb6da4e89e97e84193593630
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209403"
---
# <a name="accessing-query-context-in-stored-procedures"></a>在預存程序中存取查詢內容
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  預存程序的執行內容可做為預存程序的程式碼**內容**ADOMD.NET 伺服器物件模型的物件。 這是唯讀的內容，而且不能由預存程序加以修改。 下列屬性可以在此物件上使用。  
  
|屬性|type|描述|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|目前查詢內容的 Cube。|  
|**CurrentDatabaseName**|String|目前資料庫的識別碼。|  
|**CurrentConnection**|連接|對目前內容中之連線物件的參考。|  
|**傳遞**|Integer|目前內容的行程數目。|  
  
 **內容**物件存在，預存程序中使用多維度運算式 (MDX) 物件模型時。 如果是在用戶端上使用 MDX 物件模型，則無法使用該物件。 **內容**未明確傳遞至或預存程序傳回的物件。 在預存程序執行時可使用此物件。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型組件管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定義預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
