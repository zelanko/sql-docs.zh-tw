---
title: Analysis Services 教學課程第 3 課： 標記為日期資料表 |Microsoft 文件
description: 描述如何將標示 Analysis Services 教學課程專案中的日期資料表。
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 679e3d629bb69ce4aab067b1becc7df8af24e140
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mark-as-date-table"></a>標記為日期資料表

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在第 2 課： 取得資料，您匯入名為的維度資料表**DimDate**。 而在模型中此資料表名為 DimDate，因此可以也可稱為*日期資料表*、，其中包含日期和時間資料。  
  
每當您使用 DAX 時間智慧函數，例如當您建立量值之後，您必須指定屬性，其中包括*日期資料表*和唯一識別碼*日期資料行*該資料表中。
  
在這一課，您將標記**DimDate**資料表做為*日期資料表*和**日期**（在 Date 資料表） 的資料行，做為*日期資料行*（唯一的識別項）。  

您將日期資料表與日期資料行標記之前，是讓您的模型更易於了解一些環境維護的好時機。 請注意，在 DimDate 資料表的資料行**FullDateAlternateKey**。 此資料行包含一個資料列包含資料表中每個日曆年度中每一天。 您使用此資料行許多量值公式和報告中。 但是，FullDateAlternateKey 並非真正的良好的識別項，此資料行。 您重新命名**日期**，以便更容易識別，並包含在公式中。 可能的話，最好先重新命名資料表和資料行，使其更容易識別無法在 SSDT 和用戶端報表應用程式之類的物件。 
  
估計的時間才能完成這一課：**三分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 然後再執行工作，在這一課，您應已完成上一課：[第 2 課： 取得資料](../tutorial-tabular-1400/as-lesson-2-get-data.md)。 

### <a name="to-rename-the-fulldatealternatekey-column"></a>若要重新命名 FullDateAlternateKey 資料行

1.  在模型設計師中，按一下**DimDate**資料表。

2.  按兩下之標頭**FullDateAlternateKey**資料行，然後將它重新命名**日期**。

  
### <a name="to-set-mark-as-date-table"></a>設定標記為日期資料表  
  
1.  選取 [日期] 資料行，然後在 [屬性] 視窗的 [資料類型] 下方，確定已選取 [日期]。  
  
2.  依序按一下 [資料表] 功能表、[日期] 和 [標記為日期資料表]。  
  
3.  在 [標記為日期資料表] 對話方塊的 [日期] 清單方塊中，選取 [日期] 資料行當作唯一識別碼。 它通常會選取預設值。 按一下 **[確定]**。 

    ![as-lesson3-date-table](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>下一步

[第 4 課： 建立關聯性](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)。
  
