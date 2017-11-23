---
title: "TOM API (Analysis Services AMO-TOM) 中的錯誤處理 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ec44daa0-a90e-42ad-b70d-6a7a7a4e4b7b
caps.latest.revision: "4"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 30d824c54359a7f7db0d57f7a4a7922329a0e89b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="handling-errors-in-the-tom-api-analysis-services-amo-tom"></a>TOM API (Analysis Services AMO-TOM) 中的錯誤處理

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Managed 程式庫，例如 Analysis Services 管理物件 (AMO) 表格式物件模型 (TOM) 的常見作法是使用例外狀況做為向使用者回報錯誤狀況的機制。  

當 AMO TOM 中偵測到錯誤時，除了擲回一些標準的.NET 例外狀況就像**ArgumentException**和**InvalidOperationException**，TOM 也數個 TOM 特定例外狀況。  

TOM 例外狀況衍生自[AmoException 類別](http://msdn.microsoft.com/library/microsoft.analysisservices.amoexception.aspx)，涵蓋這兩個 AMO 和 TOM 特定的例外狀況。 

為了說明 TOM 的例外狀況處理，讓我們檢閱其中一個更常見的例外狀況，也就是[OperationException 類別](http://msdn.microsoft.com/library/microsoft.analysisservices.operationexception.aspx)。

**OperationException**使用者起始 Analysis Services 伺服器上的執行作業，伺服器無法執行作業，因為動作是不合法的或是因為發生內部或外部的其他錯誤時，會擲回。 

當擲回，* * OperationException * * 物件會包含 XMLA 伺服器所傳回的錯誤清單。 

請注意，伺服器將不會接受無效的變更。 如果發生這種情況，還原**模型**回最後的已知良好的狀態使用的樹狀結構[UndoLocalChanges 方法](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.model.undolocalchanges.aspx)，請更正模型，然後再重新送出。 

## <a name="code-example-handle-exceptions"></a>程式碼範例： 控制代碼的例外狀況 
 
```
 try 
 { 
  // Change the Model, for example create a table. 
  // … 
   model.saveChanges(); 
 } 
  catch(operationException ex) 
 { 
  foreach(XmlaError err in ex.Results.OfType<XmlaError>().cast<XmlaError>()) 
  { 
   Console.WriteLine(“Error returned from the server:” + err.Messsage ); 
  } 
 } 
```

## <a name="next-steps"></a>後續的步驟

其他相關的例外狀況包括：

- [TomInternalException 類別](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tominternalexception.aspx)
- [TomValidationException 類別](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tomvalidationexception.aspx)
- [JsonSerializationException 類別](http://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_JsonSerializationException.htm)
