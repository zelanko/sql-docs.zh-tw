---
title: Analysis Services 教學課程第 3 課： 標記為日期資料表 |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 282103baa0283e46e31b9ffe6b837e90e4bfac3c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069395"
---
# <a name="mark-as-date-table"></a>標記為日期資料表

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在第 2 課： 取得資料，您匯入名為維度資料表**DimDate**。 當您在模型中此資料表名為 DimDate 時，它可以也稱作*日期資料表*，其中包含日期和時間資料。  
  
每當您使用 DAX 時間智慧函式，例如當您建立量值之後，您必須指定屬性，其中包括*日期資料表*和唯一識別碼*日期資料行*該資料表中。
  
在這一課，您將標記**DimDate**資料表做為*日期資料表*並**日期**（在 Date 資料表中） 的資料行，做為*日期資料行*（唯一的識別項）。  

您將標記日期資料表和日期資料行之前，它是進行一些內部管理，讓您的模型更容易了解的好時機。 請注意 DimDate 資料表中的資料行**FullDateAlternateKey**。 此資料行包含一個資料列加入資料表中每個日曆年度中每一天。 您使用此資料行很多量值公式和報告中。 但是，FullDateAlternateKey 並不是此資料行的理想識別項。 您將它重新命名**日期**，讓您更輕鬆地識別和納入公式中。 可能的話，它是個不錯的主意，若要重新命名物件，例如資料表和資料行，以便於識別無法在 SSDT 和用戶端報表應用程式。 
  
估計的時間才能完成這一課：**三分鐘**  
  
## <a name="prerequisites"></a>先決條件  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 執行工作之前在這一課，您應已完成上一課：[第 2 課： 取得資料](../tutorial-tabular-1400/as-lesson-2-get-data.md)。 

### <a name="to-rename-the-fulldatealternatekey-column"></a>若要重新命名 FullDateAlternateKey 資料行

1.  在模型設計師中，按一下**DimDate**資料表。

2.  按兩下之標頭**FullDateAlternateKey**資料行，然後將它重新命名**日期**。

  
### <a name="to-set-mark-as-date-table"></a>設定標記為日期資料表  
  
1.  選取 [日期] 資料行，然後在 [屬性] 視窗的 [資料類型] 下方，確定已選取 [日期]。  
  
2.  依序按一下 [資料表] 功能表、[日期] 和 [標記為日期資料表]。  
  
3.  在 [標記為日期資料表] 對話方塊的 [日期] 清單方塊中，選取 [日期] 資料行當作唯一識別碼。 它通常會選取預設值。 按一下 [確定] 。 

    ![as-lesson3-date-table](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>下一步

[第 4 課： 建立關聯性](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)。
  
