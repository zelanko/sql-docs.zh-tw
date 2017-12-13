---
title: "存取查詢內容中的預存程序 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- execution context [Analysis Services]
- stored procedures [Analysis Services], query context
- Context object
- query context [Analysis Services]
ms.assetid: bdc7dad8-2f22-4265-aba4-a3a451527840
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a9ab0de9eae86293f25781cc5b85f175037f1ffc
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="accessing-query-context-in-stored-procedures"></a>在預存程序中存取查詢內容
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]預存程序的執行內容是可以在預存程序的程式碼中使用**內容**ADOMD.NET 伺服器物件模型的物件。 這是唯讀的內容，而且不能由預存程序加以修改。 下列屬性可以在此物件上使用。  
  
|屬性|型別|Description|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|目前查詢內容的 Cube。|  
|**CurrentDatabaseName**|字串|目前資料庫的識別碼。|  
|**CurrentConnection**|連接|對目前內容中之連線物件的參考。|  
|**傳遞**|Integer|目前內容的行程數目。|  
  
 **內容**物件存在，預存程序中使用多維度運算式 (MDX) 物件模型時。 如果是在用戶端上使用 MDX 物件模型，則無法使用該物件。 **內容**未明確傳遞至或預存程序傳回的物件。 在預存程序執行時可使用此物件。  
  
## <a name="see-also"></a>請參閱  
 [多維度模型組件管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定義預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
