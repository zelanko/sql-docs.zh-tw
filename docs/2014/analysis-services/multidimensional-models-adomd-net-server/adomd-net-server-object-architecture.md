---
title: ADOMD.NET 伺服器物件架構 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 33a8f420f985c9e62c7d7f275e7de370a6988e8d
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469053"
---
# <a name="adomdnet-server-object-architecture"></a>ADOMD.NET 伺服器物件架構
  ADOMD.NET 伺服器物件是 helper 物件，可用來在中建立使用者定義函數（Udf）或預存程式 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。  
  
> [!NOTE]  
>  若要使用 `Microsoft.AnalysisServices.AdomdServer` 命名空間 (以及這些物件)，必須將 msmgdsrv.dll 的參考加入 UDF 專案或是預存程序。  
  
 ![顯示 ADOMD.NET 伺服器中的物件關聯性](../../analysis-services/dev-guide/media/adomdnetserverobjectmodel.gif "顯示 ADOMD.NET 伺服器中的物件關聯性")  
ADOMD.NET 物件模型  
  
 與 ADOMD.NET 物件階層互動通常是從最頂層中的一或多個物件開始，如下表所述。  
  
|至|使用此物件|  
|--------|---------------------|  
|評估多維度運算式 (MDX) 的運算式|[Microsoft.analysisservices. AdomdServer. 運算式](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120))<br /> [Microsoft.analysisservices. AdomdServer 運算式](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120))物件提供一種方法，可執行 MDX 運算式，並在指定的元組下評估該運算式。|  
|提供執行 MDX 函數的支援，而無須建構完整的 MDX 陳述式。|[Microsoft.analysisservices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))<br /> [Microsoft.analysisservices. AdomdServer](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))物件很方便呼叫預先定義的 MDX 函式，而不使用[microsoft.analysisservices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120))物件。 在未來的版本中，應該可以使用[microsoft.analysisservices. AdomdServer](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))物件的其他函數。|  
|表示 UDF 目前的執行內容|[Microsoft.analysisservices. AdomdServer. 內容](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))<br /> [Microsoft.analysisservices. AdomdServer 內容](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))物件會公開資訊，例如目前的 cube 或模型和各種元資料集合。 [Microsoft.analysisservices. AdomdServer. CoNtext](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))物件的其中一個主要用途，就是 microsoft.analysisservices. CurrentMember. [microsoft.analysisservices. 階層物件的](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120)) [AdomdServer *](/previous-versions/sql/sql-server-2014/ms137044(v=sql.120))屬性。 這個主要用法可讓 UDF 或是預存程序的作者，根據查詢的對象是來自某個維度的哪個成員來做決定。|  
|建立集合和 Tuple|[Microsoft.analysisservices. AdomdServer. SetBuilder](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120))、 [microsoft microsoft.analysisservices.](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120)) AdomdServer. TupleBuilder<br /> [Microsoft.analysisservices. AdomdServer. SetBuilder](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120))提供建立不可變集合的方法，而[Microsoft microsoft.analysisservices. AdomdServer](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120))則提供建立不可變元組的方式。|  
|支援隱含轉換以及 MDX 語言的六個基本類型之間轉換。|[Microsoft.analysisservices. AdomdServer. MDXValue](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120))<br /> [Microsoft.analysisservices. AdomdServer. MDXValue](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120))物件提供下列類型之間的隱含轉換和轉換：<br /><br /> -   [Microsoft.analysisservices. AdomdServer. 階層架構](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120))<br />-   [Microsoft.analysisservices. AdomdServer. Level](/previous-versions/sql/sql-server-2014/ms143581(v=sql.120))<br />-   [Microsoft.analysisservices. AdomdServer. Member](/previous-versions/sql/sql-server-2014/ms143820(v=sql.120))<br />-   [Microsoft.analysisservices. AdomdServer. 元組](/previous-versions/sql/sql-server-2014/ms145330(v=sql.120))<br />-   [Microsoft.analysisservices. AdomdServer. Set](/previous-versions/sql/sql-server-2014/ms144530(v=sql.120))<br />-純量或實數值型別|  
  
## <a name="see-also"></a>另請參閱  
 [ADOMD.NET 伺服器程式設計](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
