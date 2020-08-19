---
description: '評定 Access 資料庫物件的轉換 (AccessToSQL) '
title: 評定 Access 資料庫物件的轉換 (AccessToSQL) |Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6bf9144249bc8707bce9c812da19a07bacc43c68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418604"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>評定 Access 資料庫物件的轉換 (AccessToSQL) 
在您載入物件並將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 之前，您應該先決定要成功的遷移量，以及轉換可能需要的時間。 SSMA 可以建立評定報告，顯示已成功轉換為的物件百分比， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 語法和執行遷移的時間估計。 SSMA 也可讓您查看造成轉換失敗的特定問題。  
  
## <a name="creating-assessment-reports"></a>建立評量報告  
當它建立評量報告時，SSMA 會將選取的 Access 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 語法，然後顯示結果。  
  
**若要建立評量報告**  
  
1.  在 [存取中繼資料瀏覽器] 中，選取您要評估的資料庫。  
  
2.  若要省略個別物件，請清除不想要評估之物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下 [ **資料庫**]，然後選取 [ **建立報告**]。  
  
    您也可以在物件上按一下滑鼠右鍵，然後選取 [ **建立報表**]，來分析個別的物件。  
  
    SSMA 會在視窗底部的狀態列中顯示進度。 如果 [輸出] 窗格是可見的，您也會在 [輸出] 窗格中看到訊息。  
  
評量完成時，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取：評定報表] 視窗的 Migration Assistant 隨即出現。  
  
## <a name="using-assessment-reports"></a>使用評量報告  
[評定報表] 視窗包含三個窗格： [explorer]、[詳細資料] 窗格和 [訊息] 窗格。  
  
-   [Explorer] 窗格可讓您流覽已評估的物件。 您可以按一下此窗格中的專案，向下切入至個別資料表、索引和索引鍵。  
  
-   詳細資料窗格會顯示所選物件的轉換統計資料。  
  
-   [訊息] 窗格會顯示轉換的錯誤、警告和參考用訊息，以及執行遷移和個別錯誤修正步驟的時間估計。  
  
您應該更正錯誤，然後再次執行評量報告或轉換架構。 若要找出錯誤，請按一下 [訊息] 窗格中的 [ **錯誤** ] 按鈕，然後展開每一個錯誤，以查看發生錯誤的物件清單。 如果您按一下 [訊息] 窗格中的物件，該物件的所有錯誤和警告都會出現在詳細資料窗格中。  
  
## <a name="next-step"></a>後續步驟  
[轉換 Access 資料庫物件](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
