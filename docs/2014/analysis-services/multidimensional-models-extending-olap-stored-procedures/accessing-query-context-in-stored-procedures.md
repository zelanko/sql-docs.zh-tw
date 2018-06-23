---
title: 存取查詢內容中的預存程序 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- execution context [Analysis Services]
- stored procedures [Analysis Services], query context
- Context object
- query context [Analysis Services]
ms.assetid: bdc7dad8-2f22-4265-aba4-a3a451527840
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ef60683eb410f0db5ba9e8d38ac227ca22dd9159
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033372"
---
# <a name="accessing-query-context-in-stored-procedures"></a>在預存程序中存取查詢內容
  預存程序的執行內容可以在該預存程序的程式碼中使用，如同 ADOMD.NET 伺服器物件模型的 `Context` 物件。 這是唯讀的內容，而且不能由預存程序加以修改。 下列屬性可以在此物件上使用。  
  
|屬性|類型|描述|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|目前查詢內容的 Cube。|  
|**CurrentDatabaseName**|String|目前資料庫的識別碼。|  
|**CurrentConnection**|連接|對目前內容中之連線物件的參考。|  
|**傳遞**|Integer|目前內容的行程數目。|  
  
 預存程序中若使用到多維度運算式 (MDX) 物件模型，會有 `Context` 物件。 如果是在用戶端上使用 MDX 物件模型，則無法使用該物件。 `Context` 物件並未明確地傳遞至預存程序，或由預存程序傳回。 在預存程序執行時可使用此物件。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型組件管理](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定義預存程序](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  