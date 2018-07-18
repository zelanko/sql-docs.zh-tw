---
title: ADOMD.NET 伺服器功能 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 003e50efa8ed21720410830a3d02134df15c3c97
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023775"
---
# <a name="adomdnet-server-functionality"></a>ADOMD.NET 伺服器功能
  所有的 ADOMD.NET 伺服器物件，都可用唯讀方式存取伺服器上的資料與中繼資料。 若要擷取資料與中繼資料，使用 ADOMD.NET 伺服器物件模型做為伺服器物件模型，並不支援結構描述資料列集。  
  
 透過 ADOMD.NET 伺服器物件，您可以建立使用者定義函數 (UDF) 或是預存程序[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 這些同處理序方法是透過以多維度運算式 (MDX)、資料採礦延伸模組 (DMX) 或是 SQL 等語言所建立的查詢陳述式來呼叫。 這些同處理序方法也提供與網路通訊關聯且沒有延遲的附加功能。  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> 物件只支援 DMX。  
  
## <a name="what-is-a-udf"></a>何謂 UDF？  
 A *UDF*是一種方法具有下列特性：  
  
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
 A*預存程序*是一種方法具有下列特性：  
  
-   您呼叫預存程序上使用 MDX 自己[呼叫](../../mdx/mdx-data-manipulation-call.md)陳述式。  
  
-   預存程序可以使用任何數目的參數。  
  
-   預存程序可以傳回資料集、 **IDataReader**，或是空的結果。  
  
 下列範例使用虛構的預存程序 `FinalSalesNumbers`：  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>另請參閱  
 [ADOMD.NET 伺服器程式設計](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
