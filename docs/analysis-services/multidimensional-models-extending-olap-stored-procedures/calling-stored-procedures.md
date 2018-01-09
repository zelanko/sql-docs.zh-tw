---
title: "呼叫預存程序 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- calling stored procedures
- stored procedures [Analysis Services], calling
- MDX queries [Analysis Services]
- CALL statement
ms.assetid: 96a9660d-875b-4ee4-b339-90020b1d9895
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0ea0a687bd6e5482211a4f953c0f7565c483a586
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="calling-stored-procedures"></a>呼叫預存程序
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]在伺服器上，或從用戶端應用程式，可以呼叫預存程序。 在這兩種情況下，預存程序永遠會在伺服器上執行，不論是伺服器或資料庫的內容。 執行預存程序並不需要特殊的權限。 組件將預存程序加入到伺服器或資料庫內容後，任何使用者都可以執行預存程序，只要使用者的角色允許該預存程序執行的動作。  
  
 在 MDX 中呼叫預存程序，與呼叫內建 MDX 函數的方式相同。 對於未採用參數的預存程序，則會使用程序名稱和空白的成對括號，如此處所示：  
  
```  
MyStoredProcedure()  
```  
  
 如果預存程序有一或多個參數，則依序提供以逗號分隔的參數。 下例展示具有三個參數的預存程序範例：  
  
```  
MyStoredProcedure("Parameter1", 2, 800)  
```  
  
## <a name="calling-stored-procedures-in-mdx-queries"></a>在 MDX 查詢中呼叫預存程序  
 在所有 MDX 查詢中，預存程序必須傳回 MDX 運算式所需的句法正確類型。 如果預存程序沒有傳回正確類型，就會發生 MDX 錯誤。 下列範例展示的預存程序會傳回數學運算的集合、成員和結果。  
  
### <a name="returning-a-set"></a>傳回集合  
 下列範例實作名稱為 MySproc 的預存程序，它會傳回一個集合。 在第一個範例中，MySproc 會在 SELECT 運算式中直接傳回集合。 其次的兩個範例中，MySproc 會將集合以 Crossjoin 和 DrilldownLevel 函數之引數的方式傳回。  
  
```  
SELECT MySetProcedure(a,b,c) ON 0 FROM Sales  
SELECT Crossjoin(MySetProcedure(a,b,c)) ON 0 FROM Sales  
SELECT DrilldownLevel(MySetProcedure(a,b,c)) ON 0 FROM Sales  
```  
  
### <a name="returning-a-member"></a>傳回成員  
 下例顯示名稱為 MySproc 的函數，它會傳回一個成員：  
  
```  
SELECT Descendants(MySproc(a,b,c),3) ON 0 FROM Sales  
```  
  
### <a name="returning-the-result-of-a-math-operation"></a>傳回數學運算的結果  
  
```  
SELECT Country.Members on 0, MySproc(Measures.Sales) ON 1 FROM Sales  
```  
  
## <a name="calling-stored-procedures-with-the-call-statement"></a>使用 CALL 陳述式呼叫預存程序  
 預存程序可以呼叫內容的 MDX 查詢使用 MDX 外部**呼叫**陳述式。  
  
 您可使用這個方法具現化預存程序的副作用，或讓應用程式取得預存查詢的結果。 常見用法**呼叫**陳述式就是使用分析管理物件 (AMO) 來執行沒有傳回結果的系統管理功能。 例如，下列命令會呼叫預存程序：  
  
```  
Call MyStoredProcedure(a,b,c)  
```  
  
 唯一支援的預存程序所傳回的型別**呼叫**陳述式是資料列集。 資料列集的序列化是由 XML for Analysis 定義的。 如果在預存程序**呼叫**陳述式會傳回任何其他型別，則會忽略，並不在 XML 中傳回呼叫的應用程式。 如需有關 XML for Analysis 資料列集的詳細資訊，請參閱＜XML for Analysis 結構描述資料列集＞。  
  
 如果預存程序傳回 .NET 資料列集，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將伺服器上的結果轉換成 XML for Analysis 資料列集。 XML for Analysis 資料列集一律會傳回在預存程序**呼叫**函式。 如果資料集包含的功能無法在 XML for Analysis 資料列集內表示，結果會失敗。  
  
 傳回空值的程序 (例如，Visual Basic 中的副程式) 也可以和 CALL 關鍵字一起使用。 例如，如果您想要在 MDX 陳述式中使用函數 MyVoidFunction()，應使用以下的語法：  
  
```  
CALL(MyVoidFunction)  
```  
  
## <a name="see-also"></a>請參閱  
 [多維度模型組件管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定義預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
