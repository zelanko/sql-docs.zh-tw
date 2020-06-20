---
title: 建立和管理量值（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
author: minewiskan
ms.author: owend
ms.openlocfilehash: fbc0d47c523be7a6a1dd421535862ac30748168a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939809"
---
# <a name="create-and-manage-measures-ssas-tabular"></a>建立及管理量值 (SSAS 表格式)
  量值是為了在報表或 Excel 樞紐分析表 (或樞紐分析圖) 中使用而建立的公式。 量值可以用標準彙總函式 (例如 COUNT 或 SUM) 做為基礎，或者，您也可以使用 DAX 自行定義公式。 本主題中的工作描述如何使用資料表的量值方格來建立和管理量值。  
  
 本主題也包括下列工作：  
  
-   [使用標準彙總公式建立量值](#bkmk_create_stand)  
  
-   [使用自訂公式建立量值](#bkmk_create_custom)  
  
-   [編輯量值屬性](#bkmk_edit)  
  
-   [重新命名量值](#bkmk_rename)  
  
-   [刪除量值](#bkmk_delete)  
  
## <a name="tasks"></a>工作  
 若要建立和管理量值，您將使用資料表的量值方格。 您只能在模型設計師的 [資料檢視] 中，檢視資料表的量值方格。 您無法在 [圖表檢視] 中建立量值或檢視量值方格；但是，您可以在 [圖表檢視] 中檢視現有的量值。 若要顯示資料表的量值方格，請按一下 **[資料表]** 功能表，然後按一下 **[顯示量值方格]**。  
  
###  <a name="to-create-a-measure-using-a-standard-aggregation-formula"></a><a name="bkmk_create_stand"></a>若要使用標準匯總公式建立量值  
  
-   依序按一下您要建立量值的資料行及 **[資料行]** 功能表，指向 **[自動加總]**，然後按一下彙總類型。  
  
     隨即會以預設名稱自動建立量值，後面接著量值方格中資料行正下方之第一個資料格的公式。  
  
###  <a name="to-create-a-measure-using-a-custom-formula"></a><a name="bkmk_create_custom"></a>若要使用自訂公式建立量值  
  
-   在量值方格中，於您要建立量值的資料行下方，按一下資料格，然後在公式列中輸入名稱，後面依序接著冒號 (:)、等號 (=) 及公式。 按下 ENTER 鍵接受公式。  
  
###  <a name="to-edit-measure-properties"></a><a name="bkmk_edit"></a>若要編輯量值屬性  
  
-   在量值方格中，按一下量值，然後在 **[屬性]** 視窗中，輸入或選取不同的屬性值。  
  
###  <a name="to-rename-a-measure"></a><a name="bkmk_rename"></a>若要重新命名量值  
  
-   在量值方格中，按一下量值，然後在 **[屬性]** 視窗的 **[量值名稱]** 中輸入新名稱，再按一下 ENTER 鍵。  
  
     您也可以在公式列中重新命名量值。 量值名稱之前為公式，後面接著冒號。  
  
###  <a name="to-delete-a-measure"></a><a name="bkmk_delete"></a>若要刪除量值  
  
-   在量值方格的量值上按一下滑鼠右鍵，然後按一下 [刪除]****。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;的量值](measures-ssas-tabular.md)   
 [&#40;SSAS 表格式&#41;的 Kpi](kpis-ssas-tabular.md)   
 [導出資料行 &#40;SSAS 表格式&#41;](ssas-calculated-columns.md)  
  
  
