---
title: 從範本建立單一預測查詢 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- singleton query predictions [DMX]
ms.assetid: e0a68ab0-bece-4d25-b464-47f1719302e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15dcb2c8241b8b4cf7cdb2780ed532e863cf52ab
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66085484"
---
# <a name="create-a-singleton-prediction-query-from-a-template"></a>根據範本建立單一預測查詢
  當您有一種模型，您想要用於預測，但不想要將它對應至外部輸入資料集，或進行大量預測時，單一查詢便很有用。 使用單一查詢，您可以向模型提供一個或多個值，並且立即會看到預測值。  
  
 例如，下列 DMX 查詢表示針對目標郵寄模型 TM_Decision_Tree 的單一查詢。  
  
```  
SELECT * FROM [TM_Decision_tree] ;  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 下列程序描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的範本總管來快速建立此查詢。  
  
### <a name="to-open-the-analysis-services-templates-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中開啟 Analysis Services 範本  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [檢視]  功能表上，按一下 [範本總管] 。  
  
2.  按一下 Cube 圖示，即可開啟 [Analysis Server] 範本。  
  
### <a name="to-open-a-prediction-query-template"></a>開啟預測查詢範本  
  
1.  在**範本總管**中，於 Analysis Server 範本的清單內，展開 [DMX]，然後展開 [預測查詢]。  
  
2.  按兩下 [單一預測]。  
  
3.  在 [連接到 Analysis Services] 對話方塊中，輸入具有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體 (包含即將進行查詢的採礦模型) 的伺服器名稱。  
  
4.  按一下 **[連接]**。  
  
5.  此範本會在指定的資料庫中開啟，並提供採礦模型物件瀏覽器，其中包含資料採礦函數和資料採礦結構與相關模型的清單。  
  
### <a name="to-customize-the-singleton-query-template"></a>自訂單一查詢範本  
  
1.  在此範本中，按一下 [可用的資料庫] 下拉式清單，然後從清單中選取 Analysis Service 的執行個體。  
  
2.  在 [採礦模型] 清單中，選取您想要查詢的採礦模型。  
  
     採礦模型中的資料行清單會顯示在物件瀏覽器的 [中繼資料] 窗格中。  
  
3.  在 [查詢] 功能表上，選取 [指定範本參數的值]。  
  
4.  在 [選取清單] 資料列中，輸入 * 以便傳回所有資料行，或輸入資料行和運算式的逗號分隔清單以便傳回特定的資料行。  
  
     如果您輸入 *，就會傳回可預測資料行，以及您在步驟 6 中提供新值的任何資料行。  
  
     若為本主題開頭所顯示的範例程式碼，[選取清單] 資料列設定為 *。  
  
5.  在 [採礦模型] 資料列中，根據**物件總管**中顯示的採礦模型清單，輸入採礦模型的名稱。  
  
     本主題開頭所顯示的範例程式碼**採礦模型**資料列設定名稱， `TM_Decision_Tree`。  
  
6.  在 [值] 資料列中，針對您想要進行預測的項目輸入新資料值。  
  
     本主題開頭所顯示的範例程式碼**值**資料列設定`2`來預測自行車購買行為，根據家中子女數目。  
  
7.  在 [資料行] 資料列中，輸入新資料應該對應至採礦模型中的目標資料行名稱。  
  
     本主題開頭所顯示的範例程式碼**資料行**資料列設定`Number Children at Home`。  
  
    > [!NOTE]  
    >  當您使用 [指定範本參數的值] 對話方塊時，不需要在資料行名稱前後加上方括號。 系統會自動為您加入括號。  
  
8.  離開**輸入的別名**做為`t`。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 在查詢文字窗格中，尋找逗號和省略符號底下的紅色不規則曲線，表示語法錯誤。 請刪除省略符號，然後加入所需的任何其他查詢條件。 如果您沒有加入任何其他條件，請刪除逗號。  
  
     若為本主題開頭所顯示的範例程式碼，其他查詢條件設定為 `'45' as [Age]`。  
  
11. 按一下 **[執行]**。  
  
## <a name="see-also"></a>另請參閱  
 [建立預測 &#40;資料採礦基本教學課程&#41;](../../tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
  
