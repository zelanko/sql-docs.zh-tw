---
title: 根據範例填滿（適用于 Excel 的資料表分析工具） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- fill from example
ms.assetid: dac57d8f-1c65-4878-8ea0-9c680df5e4fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d1e09e439469f23412c84ea7bab65c0aa748f286
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081322"
---
# <a name="fill-from-example-table-analysis-tools-for-excel"></a>根據範例填滿 (適用於 Excel 的資料表分析工具)
  ![資料表分析工具中的根據範例填滿按鈕](media/tat-fillex.gif "資料表分析工具中的根據範例填滿按鈕")  
  
 [**根據範例填滿**] 工具可協助您根據現有的值建立新的資料行。  
  
 例如，假設您的資料包含 [**採購金額**] 資料行、[**訂單數量**] 資料行和 [**頂級客戶**] 資料行，其以使用其他資料行的公式為基礎。 如果 [**頂級客戶**] 資料行包含許多空白資料列，您可以使用 [**購買數量**] 和 [**訂單數量**] 欄做為輸入，以推斷遺漏的值。 此工具會分析資料中現有的模式連同您所輸入的範例，並且預測每個客戶將獲指派的分類。  
  
 如果您對結果感到不滿意，可提供更多範例來改善結果。  
  
## <a name="using-the-fill-from-example-tool"></a>使用根據範例填滿工具  
  
1.  在 [**分析**] 功能區中，按一下 [**根據範例填滿**]。  
  
2.  此工具將會根據資料分析自動挑選要填滿的資料行，而且您可以接受或覆寫這項建議。  
  
3.  為新的資料建立資料行，並輸入您所要預測的資料範例。 確定您所要預測的每個值至少都有一個範例。 如果是在將資料填滿到現有的資料行中，請選取具有遺失值的資料行。  
  
4.  （選擇性）按一下 **[選擇要用於分析的資料行**]。 在 [資料**行選取範圍**] 對話方塊中，指定填入遺漏的資料時，最有可能有用的資料行。  
  
     例如，如果您從經驗得知，某個資料行與另一個具有遺失值的資料行之間有因果關係，即可取消選取其他資料行來獲得更好的結果。  
  
     按一下 [確定]  。  
  
5.  按一下 **[執行]** 。  
  
     分析完成時，工具會建立新的**模式**工作表，其中包含分析的結果。 此報表會列出找到的規則或關鍵影響因數，並且顯示每個規則的機率。  
  
     此工具也會將包含新值的資料行加入到原始的資料表。 您可以檢閱這些值，並且將其與原始的值比較。  
  
### <a name="requirements"></a>需求  
 您只能使用在資料行中的資料。 如果您要填滿的數列存放在資料列中，您可以使用 Excel 中的 Paste、Transpose 函數將資料變更為單欄式格式。  
  
## <a name="understanding-the-pattern-report"></a>了解模式報表  
 當您執行 [**根據範例填滿**] 工具時，會建立一份報告，提供所偵測到之模式的詳細資訊。 這些模式會用於推斷新的資料值。  
  
 模式報表會顯示所預測之每個值的關鍵影響因數。 每個影響因數或規則都會被描述為資料行、該資料行中的值，以及規則對於預測之相對影響的組合。  
  
 例如，如果您嘗試填滿顯示訂單運輸距離的工作表，便能在邏輯上期待目的地會對運輸距離值具有強烈影響。 在此情況下，報表可能會包含以下資料列：  
  
|資料行|值|喜好|相對影響|  
|------------|-----------|------------|---------------------|  
|StateProvinceCode|AB|>500 公里|80%|  
  
 這表示**StateProvinceCode**資料行中的值 AB 會強烈預測 >500 公里的出貨距離。  
  
 通常，預測都會根據複雜度遠勝於此範例的模式，而且報表可能會針對每項預測包含許多規則資料列。 所有規則的效果都會組合以衍生出預測值。  
  
> [!NOTE]  
>  **相對影響**會顯示為陰影橫條。 該橫條越長，這條規則也就越有可能是填滿值的預測。  
  
 此工具也會將新的資料行加入至原始資料表， \<名為 column name，> 擴充。  
  
 如果原始的資料資料行包含某個值，該值便會複製到新資料行中。 不過，如果原始的資料行包含空白的儲存格，新資料行便會包含由精靈所預測的值。  
  
## <a name="related-tools-and-information"></a>相關工具和資訊  
 您也可以使用 [適用于 Excel 的資料採礦用戶端] 中的 [[流覽資料](explore-data-sql-server-data-mining-add-ins.md)] wizard，檢查 excel 資料行中的值分佈。 如需詳細資訊，請參閱[探索和清除資料](exploring-and-cleaning-data.md)。  
  
## <a name="see-also"></a>另請參閱  
 [適用於 Excel 的資料表分析工具](table-analysis-tools-for-excel.md)  
  
  
