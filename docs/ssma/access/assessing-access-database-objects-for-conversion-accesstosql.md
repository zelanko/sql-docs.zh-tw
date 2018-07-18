---
title: 評定 Access 資料庫物件的轉換 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- assessing SQL
- assessing syntax
- assessment reports
- creating assessment reports
- estimating migration effort
- reports
- SQL, assessing
- syntax, assessing
ms.assetid: 8b9e23d6-da62-437a-8c05-8ad2628b9441
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d2d804734432cfd396acb017d6358310debeec1f
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979420"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>評定 Access 資料庫物件的轉換 (AccessToSQL)
在您載入的物件，並將資料移轉至之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您應該判斷多少的移轉將會成功，並轉換可能會花多少時間。 SSMA 可以建立顯示之物件的成功轉換為百分比的評定報告[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的語法和時間的估計值執行移轉。 SSMA 也可讓您檢視導致轉換失敗的特定問題。  
  
## <a name="creating-assessment-reports"></a>建立評定報表  
當它所建立的評估報告 SSMA 會將轉換至所選的 Access 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的語法，然後顯示結果。  
  
**若要建立的評估報告**  
  
1.  在存取中繼資料總管 中，選取您想要評估的資料庫。  
  
2.  若要省略個別物件，清除您不想要評估的物件旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下**資料庫**，然後選取**建立報表**。  
  
    您也可以分析個別的物件，以滑鼠右鍵按一下物件，然後選取**建立報表**。  
  
    SSMA 會顯示在視窗底部的 [狀態] 列中的進度。 如果 [輸出] 窗格為可見，您也會看到 [輸出] 窗格中的訊息。  
  
當評估完成時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Access： 評定報告 視窗隨即出現。  
  
## <a name="using-assessment-reports"></a>使用評估報告  
評定報告視窗包含三個窗格： 總管 中，詳細資料窗格中，訊息窗格。  
  
-   [總管] 窗格可讓您瀏覽所評估的物件。 您可以按一下此窗格，即可向下鑽研至個別資料表、 索引和索引鍵中的項目。  
  
-   [詳細資料] 窗格會顯示所選物件的轉換統計資料。  
  
-   [訊息] 窗格會顯示錯誤、 警告和參考用訊息，轉換，和時間估計的移轉和個別錯誤更正步驟執行。  
  
您應該先更正錯誤，然後才能再次執行評定報表或將結構描述轉換。 若要尋找錯誤，請按一下**錯誤**訊息] 窗格中的按鈕，然後展開 [若要檢視發生錯誤的物件清單的每個錯誤。 如果您按一下 [訊息] 窗格中的物件時，所有錯誤和警告，該物件會都出現在 [詳細資料] 窗格中。  
  
## <a name="next-step"></a>下一個步驟  
[轉換 Access 資料庫物件](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
