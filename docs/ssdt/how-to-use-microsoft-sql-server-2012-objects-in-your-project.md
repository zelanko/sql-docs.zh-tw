---
title: 如何：在專案中使用 Microsoft SQL Server 2012 物件 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9baf122f-cf22-4860-98db-ef782cd972fc
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 319abf02d87a12e8df96e6e22666da54ade16d1d
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084500"
---
# <a name="how-to-use-microsoft-sql-server-2012-objects-in-your-project"></a>如何：在專案中使用 Microsoft SQL Server 2012 物件
在這個範例中，您會將一個序列物件加入至以 Microsoft SQL Server 2012 為目標的資料庫專案。  
  
序列在 Microsoft SQL Server 2012 中導入。 序列是使用者定義的結構描述繫結物件，該物件會根據建立順序所使用的規格產生數值序列。 數值序列是在定義的間隔依照遞增或遞減順序來產生，而且可依照要求循環 (重複)。  如需有關序列物件的詳細資訊，請參閱[序號](htttp://msdn.microsoft.com/en-us/library/ff878058(SQL.110).aspx)。 如需 Microsoft SQL Server 2012 之新功能的資訊，請參閱 [SQL Server 2012 的新功能](http://msdn.microsoft.com/en-us/library/bb500435(SQL.110).aspx)。  
  
> [!WARNING]  
> 下列程序利用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-add-a-new-sequence-object-to-your-project"></a>若要將新的序列物件加入至專案  
  
1.  以滑鼠右鍵按一下 [方案總管] 中的 [TradeDev] 資料庫專案，再依序選取 [加入] 和 [新增項目]。  
  
2.  按一下左窗格中的 [可程式性]，然後選取 [序列]。 按一下 [加入] 將新的物件加入至專案。  
  
3.  以下列程式碼取代預設程式碼。  
  
    ```  
    CREATE SEQUENCE [dbo].[Seq1]  
    AS INT  
    START WITH 1  
    INCREMENT BY 1  
    MAXVALUE 1000  
    NO CYCLE  
    CACHE 10  
    ```  
  
4.  如果專案的目標平台未設定為 Microsoft SQL Server 2012，[錯誤清單] 會顯示 `CREATE SEQUENCE` 陳述式有語法錯誤。 若要修正此問題，請遵循[如何：變更目標平台及發行資料庫專案](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)主題來相應地變更目標平台。  
  
5.  請遵循[如何：變更目標平台及發行資料庫專案](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)，將專案發佈至已連接的 Microsoft SQL Server 2012 伺服器中的資料庫。  
  
### <a name="to-use-the-new-sequence-object"></a>若要使用新的序列物件  
  
1.  在 [SQL Server 物件總管] 中，以滑鼠右鍵按一下您在上述程序中已發行的目標資料庫，再選取 [新增查詢]。  
  
2.  將下列程式碼貼入查詢視窗。  
  
    ```  
    DECLARE @counter INT  
    SET @counter=0  
    WHILE @counter<10  
    BEGIN  
        SET @counter = @counter +1  
         INSERT dbo.Products (Id, Name, CustomerId) VALUES (NEXT VALUE FOR dbo.Seq1, 'ProductItem'+cast(@counter as varchar), 1)  
    END   
    GO  
    ```  
  
3.  按 [執行查詢] 按鈕。  
  
4.  在 [SQL Server 物件總管] 中，巡覽至資料庫的 [Products] 資料表。 按一下滑鼠右鍵選取 [檢視資料] 檢查新加入的資料列。  
  
