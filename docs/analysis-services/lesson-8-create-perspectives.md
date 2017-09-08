---
title: "第 9 課建立的檢視方塊 |Microsoft 文件"
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
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 993cf02a47240c0a74667f6220c6b2dd5d6df86c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-8-create-perspectives"></a>第 8 課： 建立檢視方塊
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將建立一個 [網際網路銷售] 檢視方塊。 檢視方塊會定義可檢視之模型的子集，而這類子集會提供有焦點的商務特有或應用程式特有視點。 當使用者連接到模型使用檢視方塊時，他們可以看到只有模型的物件 （資料表、 資料行、 量值、 階層和 Kpi） 做為該檢視方塊中所定義的欄位。  
  
您在這一課中建立的網際網路銷售檢視方塊會排除 DimCustomer 資料表物件。 當您建立從檢視表中排除某些物件的檢視方塊時，該物件仍然會存在於模型中，但是在報表用戶端欄位清單中看不到。 導出資料行嗨量值無論是否包含在檢視方塊中，都仍然可以從遭排除之物件資料中計算。  
  
本課程的目的在於描述如何建立檢視方塊，以及熟悉表格式模型撰寫工具。 如果您之後展開此模型納入其他資料表，您可以建立其他檢視方塊來定義，例如存貨和銷售不同的模型，視點。 若要進一步了解，請參閱[檢視方塊](../analysis-services/tabular-models/perspectives-ssas-tabular.md)。  
  
完成本課程的估計時間： **5 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 然後再執行工作，在這一課，您應已完成上一課：[第 7 課： 建立關鍵效能指標](../analysis-services/lesson-7-create-key-performance-indicators.md)。  
  
## <a name="create-perspectives"></a>建立檢視方塊  
  
#### <a name="to-create-an-internet-sales-perspective"></a>若要建立網際網路銷售檢視方塊  
  
1.  按一下**模型**功能表 >**檢視方塊** > **建立和管理**。  
  
2.  在 [檢視方塊] 對話方塊中，按一下 [新增檢視方塊]。  
  
3.  按兩下**新檢視方塊**欄標題，並將其重新命名**Internet Sales**。  
  
4.  選取資料表的所有*除了* **DimCustomer**。  
  
    ![做為表格式-lesson8-檢視方塊](../analysis-services/media/as-tabular-lesson8-perspectives.png)
  
    在後面的課程，您將使用在 excel 中進行分析 來測試此檢視方塊。 Excel 樞紐分析表欄位清單將包含除了 DimCustomer 資料表的每個資料表。  

## <a name="whats-next"></a>下一步
移至下一課：[第 9 課： 建立階層](../analysis-services/lesson-9-create-hierarchies.md)。
  
  
  
  

