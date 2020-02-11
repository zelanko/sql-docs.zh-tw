---
title: 評估 Access 資料庫物件的轉換（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4c2f5bc6953ab0e96397ca728391cbe22a73dd50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910695"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>評估 Access 資料庫物件的轉換（AccessToSQL）
在您載入物件並將資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至或 SQL Azure 之前，您應該先判斷遷移成功的程度，以及轉換可能需要多久的時間。 SSMA 可以建立評量報告，顯示已成功轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的物件百分比，或 SQL Azure 語法和時間估計以執行遷移。 SSMA 也可讓您查看導致轉換失敗的特定問題。  
  
## <a name="creating-assessment-reports"></a>建立評量報告  
當它建立評量報告時，SSMA 會將選取的 Access 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件轉換成或 SQL Azure 語法，然後顯示結果。  
  
**若要建立評量報告**  
  
1.  在 [存取中繼資料 Explorer] 中，選取您想要評估的資料庫。  
  
2.  若要省略個別物件，請清除您不想要評估之物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下 [**資料庫**]，然後選取 [**建立報表**]。  
  
    您也可以用滑鼠右鍵按一下物件，然後選取 [**建立報表**]，來分析個別物件。  
  
    SSMA 會在視窗底部的狀態列中顯示進度。 如果顯示 [輸出] 窗格，您也會在 [輸出] 窗格中看到訊息。  
  
當評估完成時，[存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的移轉小幫手：評估報告] 視窗隨即出現。  
  
## <a name="using-assessment-reports"></a>使用評量報告  
[評估報告] 視窗包含三個窗格： [explorer]、[詳細資料] 窗格和 [訊息] 窗格。  
  
-   [Explorer] 窗格可讓您流覽已評估的物件。 您可以按一下此窗格中的專案，向下切入至個別的資料表、索引和索引鍵。  
  
-   [詳細資料] 窗格會顯示所選取物件的轉換統計資料。  
  
-   [訊息] 窗格會顯示轉換的錯誤、警告和參考用訊息，以及執行「遷移」和「個別錯誤更正」步驟的時間預估。  
  
您應該先更正錯誤，再重新執行評量報告或轉換架構。 若要找出錯誤，請按一下 [訊息] 窗格中的 [**錯誤**] 按鈕，然後展開每個錯誤，以查看發生錯誤的物件清單。 如果您按一下 [訊息] 窗格中的物件，該物件的所有錯誤和警告都會出現在詳細資料窗格中。  
  
## <a name="next-step"></a>後續步驟  
[轉換 Access 資料庫物件](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
