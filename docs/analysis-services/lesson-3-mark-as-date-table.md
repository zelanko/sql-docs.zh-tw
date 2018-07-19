---
title: 第 4 課： 標記為日期資料表 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77f29250621485f5606a0bf33615e8d15eb7d80b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057806"
---
# <a name="lesson-3-mark-as-date-table"></a>第 3 課： 標記為日期資料表
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在「第 2 課：加入資料」中，您已匯入了名為 DimDate 的維度資料表。 當您在模型中此資料表名為 DimDate 時，它可以也稱作*日期資料表*，其中包含日期和時間資料。  
  
每當您使用 DAX 時間智慧函數計算中，像您將會執行您的量值稍後建立時，您必須指定日期資料表屬性，其中包含*日期資料表*和唯一識別碼*日期資料行*該資料表中。
  
在這一課，您將 DimDate 資料表標記為*日期資料表*和日期資料行 （在 Date 資料表中），做為*日期資料行*（唯一識別碼）。  

我們在標記日期資料表和日期資料行之前，我們需要進行一些內部管理，讓您更輕鬆地了解我們的模型。 您會注意到在 DimDate 資料表中的資料行**FullDateAlternateKey**。 它可以包含一個資料列加入資料表中每個日曆年度中每一天。 我們將使用此資料行很多量值公式和報告中。 但是，FullDateAlternateKey 其實不是此資料行的理想識別項。 我們將會重新命名為**日期**，讓您更輕鬆地識別和納入公式中。 可能的話，它是個不錯的主意，若要重新命名物件，例如資料表和資料行，以便更輕鬆識別在報表 Power BI 和 Excel 等應用程式的用戶端。 
  
完成本課程的估計時間： **3 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 2 課： 將資料加入](../analysis-services/lesson-2-add-data.md)。 

### <a name="to-rename-the-fulldatealternatekey-column"></a>若要重新命名 FullDateAlternateKey 資料行

1.  在模型設計師中，按一下**DimDate**資料表。

2.  按兩下之標頭**FullDateAlternateKey**資料行，然後將它重新命名**日期**。

  
### <a name="to-set-mark-as-date-table"></a>設定標記為日期資料表  
  
1.  選取 [日期] 資料行，然後在 [屬性] 視窗的 [資料類型] 下方，確定已選取 [日期]。  
  
2.  依序按一下 [資料表] 功能表、[日期] 和 [標記為日期資料表]。  
  
3.  在 [標記為日期資料表] 對話方塊的 [日期] 清單方塊中，選取 [日期] 資料行當作唯一識別碼。 它通常會選取預設。 按一下 [確定] 。 

    ![為表格式-lesson3-日期-資料表](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>下一步
移至下一個課程︰[第 4 課： 建立關聯性](../analysis-services/lesson-4-create-relationships.md)。
  
