---
title: "第 4 課： 標記為日期資料表 |Microsoft 文件"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5bef08da2c79aa1b17241300d1b9b31e7b977781
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-3-mark-as-date-table"></a>第 3 課： 標記為日期資料表
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在「第 2 課：加入資料」中，您已匯入了名為 DimDate 的維度資料表。 而在模型中此資料表名為 DimDate，因此可以也可稱為*日期資料表*、，其中包含日期和時間資料。  
  
每當使用 DAX 時間智慧函數中的計算，因為當您建立量值的方式稍有更新版本，您將會執行，您必須指定日期資料表屬性，其中包括*日期資料表*和唯一識別碼*日期資料行*該資料表中。
  
在這一課，您將 DimDate 資料表標記為*日期資料表*和日期資料行 （在 Date 資料表），做為*日期資料行*（唯一識別碼）。  

我們將日期資料表與日期資料行之前，我們要做一些內部管理讓您更輕鬆地了解我們的模型。 您會注意到與 DimDate 資料表中的資料行**FullDateAlternateKey**。 它包含一個資料列包含資料表中每個日曆年度中每一天。 我們將使用此資料行的許多量值公式和報告中。 但是，FullDateAlternateKey 其實不是很好的識別項，此資料行。 我們將它重新命名為**日期**，以便更容易識別，並包含在公式中。 可能的話，最好先重新命名物件，例如資料表和資料行，使其更容易分辨用戶端報表應用程式，例如 Power BI 與 Excel 中。 
  
完成本課程的估計時間： **3 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 然後再執行工作，在這一課，您應已完成上一課：[第 2 課： 將資料加入](../analysis-services/lesson-2-add-data.md)。 

### <a name="to-rename-the-fulldatealternatekey-column"></a>若要重新命名 FullDateAlternateKey 資料行

1.  在模型設計師中，按一下**DimDate**資料表。

2.  按兩下之標頭**FullDateAlternateKey**資料行，然後將它重新命名**日期**。

  
### <a name="to-set-mark-as-date-table"></a>設定標記為日期資料表  
  
1.  選取 [日期] 資料行，然後在 [屬性] 視窗的 [資料類型] 下方，確定已選取 [日期]。  
  
2.  依序按一下 [資料表] 功能表、[日期] 和 [標記為日期資料表]。  
  
3.  在 [標記為日期資料表] 對話方塊的 [日期] 清單方塊中，選取 [日期] 資料行當作唯一識別碼。 它通常會選取預設的。 按一下 **[確定]**。 

    ![做為表格式-lesson3-日期的資料表](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>下一步
移至下一課：[第 4 課： 建立關聯性](../analysis-services/lesson-4-create-relationships.md)。
  

