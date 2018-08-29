---
title: Analysis Services 教學課程課程 8： 建立檢視方塊 |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 080b20dbcf7438d26102a3bf906256343271af45
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43085319"
---
# <a name="create-perspectives"></a>建立檢視方塊

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您會建立網際網路銷售檢視方塊。 檢視方塊會定義可檢視之模型的子集，而這類子集會提供有焦點的商務特有或應用程式特有視點。 當使用者連接至模型使用檢視方塊時，他們會看到只有那些模型物件 （資料表、 資料行、 量值、 階層及 Kpi） 做為該檢視方塊中所定義的欄位。 若要進一步了解，請參閱[檢視方塊](../tabular-models/perspectives-ssas-tabular.md)。
  
您在這一課中建立網際網路銷售檢視方塊會排除 DimCustomer 資料表物件。 當您建立從檢視中排除某些物件的檢視方塊時，該物件仍然存在於模型中。 不過，不顯示在報告的用戶端欄位清單。 導出資料行嗨量值無論是否包含在檢視方塊中，都仍然可以從遭排除之物件資料中計算。  
  
本課程的目的在於描述如何建立檢視方塊，以及熟悉表格式模型撰寫工具。 如果您之後展開此模型納入其他資料表，您可以建立其他檢視方塊來定義不同觀點的模型，例如，庫存與銷售。  
  
估計的時間才能完成這一課：**五分鐘**  
  
## <a name="prerequisites"></a>先決條件  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 執行工作之前在這一課，您應已完成上一課：[第 7 課： 建立關鍵效能指標](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)。  
  
## <a name="create-perspectives"></a>建立檢視方塊  
  
#### <a name="to-create-an-internet-sales-perspective"></a>若要建立網際網路銷售檢視方塊  
  
1.  按一下 **模型**功能表 >**觀點** > **建立及管理**。  
  
2.  在 [檢視方塊] 對話方塊中，按一下 [新增檢視方塊]。  
  
3.  按兩下**新的檢視方塊**資料行標題，然後重新命名**網際網路銷售**。  
  
4.  選取所有資料表*除了* **DimCustomer**。  
  
    ![as-lesson8-perspectives](../tutorial-tabular-1400/media/as-lesson8-perspectives.png)
  
    在後面的課程，您使用分析在 Excel 功能來測試此檢視方塊。 Excel 樞紐分析表欄位清單會包含除了 DimCustomer 資料表以外的每個資料表。  

## <a name="whats-next"></a>下一步

[第 9 課： 建立階層](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)。
  
  
  
  
