---
title: 第 8 課建立的檢視方塊 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f68e51be75e84226dd0b1fd3e578fa4031eda04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403520"
---
# <a name="lesson-8-create-perspectives"></a>第 8 課：建立檢視方塊
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將建立一個 [網際網路銷售] 檢視方塊。 檢視方塊會定義可檢視之模型的子集，而這類子集會提供有焦點的商務特有或應用程式特有視點。 當使用者連接至模型使用檢視方塊時，他們會看到只有那些模型物件 （資料表、 資料行、 量值、 階層及 Kpi） 做為該檢視方塊中所定義的欄位。  
  
您在這一課中建立網際網路銷售檢視方塊會排除 DimCustomer 資料表物件。 當您建立從檢視表中排除某些物件的檢視方塊時，該物件仍然會存在於模型中，但是在報表用戶端欄位清單中看不到。 導出資料行嗨量值無論是否包含在檢視方塊中，都仍然可以從遭排除之物件資料中計算。  
  
本課程的目的在於描述如何建立檢視方塊，以及熟悉表格式模型撰寫工具。 如果您之後展開此模型納入其他資料表，您可以建立其他檢視方塊來定義不同觀點的模型，例如，庫存與銷售。 若要進一步了解，請參閱[檢視方塊](../tabular-models/perspectives-ssas-tabular.md)。  
  
估計的時間才能完成這一課：**5 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 7 課：建立關鍵效能指標](lesson-7-create-key-performance-indicators.md)。  
  
## <a name="create-perspectives"></a>建立檢視方塊  
  
#### <a name="to-create-an-internet-sales-perspective"></a>若要建立網際網路銷售檢視方塊  
  
1.  按一下 **模型**功能表 >**觀點** > **建立及管理**。  
  
2.  在 [檢視方塊]  對話方塊中，按一下 [新增檢視方塊]  。  
  
3.  按兩下**新的檢視方塊**資料行標題，然後重新命名**網際網路銷售**。  
  
4.  選取資料表的所有*除了* **DimCustomer**。  
  
    ![as-tabular-lesson8-perspectives](media/as-tabular-lesson8-perspectives.png)
  
    在後面的課程，您將使用 Excel 功能中進行分析 來測試此檢視方塊。 Excel 樞紐分析表欄位清單會包含除了 DimCustomer 資料表以外的每個資料表。  

## <a name="whats-next"></a>下一步
請移至下一課：[第 9 課：建立階層](lesson-9-create-hierarchies.md)。
  
  
  
  
