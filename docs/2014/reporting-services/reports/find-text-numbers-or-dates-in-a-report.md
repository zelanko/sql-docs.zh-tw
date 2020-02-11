---
title: 在報表中尋找文字、數位或日期（SharePoint 整合模式中的 Reporting Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- searching reports
ms.assetid: 309dffe5-00f5-404f-bb63-9e6046253ae0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6cf40f4d3baa60caa0d9d44f372e41521497e33e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102673"
---
# <a name="find-text-numbers-or-dates-in-a-report-reporting-services-in-sharepoint-integrated-mode"></a>在報表中尋找文字、數字或日期 (SharePoint 整合模式的 Reporting Services)
  您可以透過輸入想要尋找的單字或片語 (搜尋詞彙的最大值為 256 個字元)，搜尋報表中的內容。 搜尋是一項導覽技術，可尋找報表中相符的值並將焦點放在包含該值的報表內容上。  
  
 搜尋不區分大小寫，而且會從目前選取的頁面或區段開始搜尋。 搜尋作業只會包含報表中顯示的內容。 如果報表包含您展開或摺疊的區域，則進行搜尋時，就會略過已摺疊區域中的值。 您只能搜尋位於目前報表中的文字、數字或日期。 如果您使用自動產生的點選連結報表來瀏覽資料，就無法在先前產生的報表上搜尋看過的詞彙，也無法使用搜尋在資料路徑中進一步向下尋找可能顯示在報表中的詞彙。  
  
 輸入要搜尋的值時，請輸入您預期會顯示在報表中的值。 除非您預期句子中的每個字都會出現在報表中，否則請勿提出疑問句 (例如，「本月份的平均收益有多少」)。  
  
 您一次只能搜尋一個詞彙或值， 不能使用搜尋運算子 (例如 AND 或 OR)，或是符號和萬用字元， 也不能執行資料的交叉搜尋 (例如，搜尋特定產品在特定月份的淨銷售額)。 如需該分析類型，請使用報表產生器來建立或使用點選連結報表。  
  
 限制存取報表資料的資料庫和模型安全性設定會套用至搜尋作業。 如果您要在使用模型做為資料來源的點選連結報表中搜尋值，但卻沒有該模型某些部分的存取權，搜尋時將會排除這些模型部分所代表的資料。  
  
### <a name="to-find-data-in-a-report"></a>在報表中尋找資料  
  
1.  開啟報表。  
  
2.  在報表工具列中，輸入您要尋找的文字、數字或日期。  
  
     如果沒有看到報表工具列，表示系統已因為某種目的將工具列隱藏起來，而且您不能使用工具列提供的功能。 此工具列的顯示狀態是由報表檢視器 Web 組件上的屬性決定。  
  
3.  按一下 **[尋找]** 。  
  
4.  若要搜尋相同值的下一個出現位置，請按 **[下一個]** 。  
  
## <a name="see-also"></a>另請參閱  
 [將報表檢視器網頁組件加入至網頁 &#40;SharePoint 整合模式的 Reporting Services&#41;](../report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
