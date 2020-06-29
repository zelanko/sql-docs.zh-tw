---
title: ADOMD.NET 伺服器功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: b74c6957-3f64-4e09-aa09-d06ee93f82fa
author: minewiskan
ms.author: owend
ms.openlocfilehash: f00215c6bcc0104c920be29e0837288a469b252e
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469073"
---
# <a name="adomdnet-server-functionality"></a>ADOMD.NET 伺服器功能
  所有的 ADOMD.NET 伺服器物件，都可用唯讀方式存取伺服器上的資料與中繼資料。 若要擷取資料與中繼資料，使用 ADOMD.NET 伺服器物件模型做為伺服器物件模型，並不支援結構描述資料列集。  
  
 使用 ADOMD.NET 伺服器物件，您可以建立使用者定義函數（UDF）或的預存程式 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 這些同處理序方法是透過以多維度運算式 (MDX)、資料採礦延伸模組 (DMX) 或是 SQL 等語言所建立的查詢陳述式來呼叫。 這些同處理序方法也提供與網路通訊關聯且沒有延遲的附加功能。  
  
> [!NOTE]  
>  [Microsoft.analysisservices. AdomdServer. AdomdCommand](/previous-versions/sql/sql-server-2014/ms143286(v=sql.120))物件僅支援 DMX。  
  
## <a name="what-is-a-udf"></a>何謂 UDF？  
 *UDF*是具有下列特性的方法：  
  
-   您可以在查詢內容中呼叫 UDF。  
  
-   UDF 可以採取任何數目的參數。  
  
-   UDF 可以傳回各種類型的資料。  
  
 下列範例使用虛構的 UDF `FinalSalesNumber`：  
  
```  
SELECT SalesPerson.Name ON ROWS,  
       FinalSalesNumber() ON COLUMNS  
FROM SalesModel  
```  
  
## <a name="what-is-a-stored-procedure"></a>何謂預存程序？  
 *預存*程式是具有下列特性的方法：  
  
-   您可以使用 MDX [call](/sql/mdx/mdx-data-manipulation-call)語句，自行呼叫預存程式。  
  
-   預存程序可以使用任何數目的參數。  
  
-   預存程序可以傳回資料集、`IDataReader` 或是空的結果。  
  
 下列範例使用虛構的預存程序 `FinalSalesNumbers`：  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>另請參閱  
 [ADOMD.NET 伺服器程式設計](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
