---
title: "輸入搜尋值的規則 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time [SQL Server], searches
- date searches
- dates [SQL Server], searches
- embedding apostrophes [SQL Server]
- logical value searches [SQL Server]
- case-sensitive search matches
- search criteria [SQL Server], rules
- text value searches [SQL Server]
- numeric value searches [SQL Server]
ms.assetid: 3c8134b7-83f4-41b4-99c8-e3949a685ff5
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 96cd179445fcab211321ccf4e89f6fbce5792230
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="rules-for-entering-search-values-visual-database-tools"></a>輸入搜尋值的規則 (Visual Database Tools)
本主題會討論輸入下列搜尋條件的常值類型時必須使用的規格：  
  
-   文字值  
  
-   數字值  
  
-   日期  
  
-   邏輯值  
  
> [!NOTE]  
> 本主題中的資訊衍生自標準 SQL-92 的規則。 不過，每一個資料庫都可以用自己的方式實作 SQL。 因此，這裡提供的準則不一定適用於所有的情況。 如果對於在特定資料庫輸入搜尋值有任何的疑問，請參考您所使用的資料庫文件。  
  
## <a name="searching-on-text-values"></a>搜尋文字值  
下列準則適用於在搜尋條件中輸入文字值時：  
  
-   **引號** ：以單引號括住文字值，例如以下的姓氏範例：  
  
    ```  
    'Smith'  
    ```  
  
    如果您是在 [準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中輸入搜尋條件，則可以只輸入文字值，查詢和檢視表設計工具會自動在前後加上單引號。  
  
    > [!NOTE]  
    > 在某些資料庫中，單引號中的詞會被視為常值，而雙引號中的詞會被視為資料行或資料表參考之類的資料庫物件。 因此，即使 [查詢和檢視設計師] 可以接受以雙引號括住的詞，其解譯的結果可能會和您的預期不同。  
  
-   **嵌入單引號** ：如果您要搜尋的資料包含單引號 (')，您可以輸入兩個單引號以表示您輸入的確實是單引號的常值，不是分隔符號。 例如，以下條件會搜尋「Swann's Way」這個值：  
  
    ```  
    ='Swann''s Way'  
    ```  
  
-   **長度限制** ：輸入長字串時，不要超過您資料庫 SQL 陳述式的最大長度。  
  
-   **區分大小寫** ：遵照您使用的資料庫的區分大小寫規則。 您使用的資料庫決定了文字搜尋是否區分大小寫。 例如，有些資料庫將運算子「=」解譯為大小寫完全相符，但是有些資料庫則允許任何大小寫字元組合都相符。  
  
    如果您不確定資料庫是否使用區分大小寫搜尋，可以在搜尋條件中使用 UPPER 或 LOWER 函數轉換搜尋資料的大小寫，如以下範例所示：  
  
    ```  
    WHERE UPPER(lname) = 'SMITH'  
    ```  
  
## <a name="searching-on-numeric-values"></a>搜尋數字值  
下列準則適用於在搜尋條件中輸入數字值時：  
  
-   **引號**：不要用引號括住數字。  
  
-   **非數字字元**：除了小數分隔符號 (在 Windows [控制台] 的 [地區設定] 對話方塊中所定義) 和負號 (-) 以外，不要包含非數字字元。 不要包含數字分位符號 (例如千位用逗號分開) 或貨幣符號。  
  
-   **小數符號** ：如果是輸入整數，可以包含小數符號，不論您搜尋的值是整數或實數。  
  
-   **科學記號** ：可以使用科學記號輸入非常大或非常小的數字，如以下例子所示：  
  
    ```  
    > 1.23456e-9  
    ```  
  
## <a name="searching-on-dates"></a>搜尋日期  
用來輸入日期的格式是依您使用的資料庫和 [查詢和檢視設計師] 中是在哪個窗格輸入日期而定。  
  
> [!NOTE]  
> 如果您不知道資料來源所用的格式為何，請在 [準則] 窗格的篩選條件資料行中，以任何您熟悉的格式輸入日期。 設計工具會將大部份這類的輸入項目轉換成適當格式。  
  
[查詢和檢視設計師] 可以使用下列的日期格式：  
  
-   **地區設定特性** (Locale-Specific)：在 [Windows 區域設定內容] 對話方塊中指定的日期格式。  
  
-   **資料庫特性**：資料庫能夠辨識的任何格式。  
  
-   **ANSI 標準日期** ：使用括號、標記「d」來指定日期和日期字串的格式，如以下例子所示：  
  
    ```  
    { d '1990-12-31' }  
    ```  
  
-   **ANSI 標準日期時間** ：類似於 ANSI 標準日期，但是不用「d」，改用「ts」，並且在日期中加入時、分及秒 (使用 24 小時格式的時鐘)，例如以下例子的 1990 年 12 月 31 日：  
  
    ```  
    { ts '1990-12-31 00:00:00' }  
    ```  
  
    ANSI 標準日期格式通常是用於以真實日期資料類型代表日期的資料庫。 相較之下，日期時間格式則是用於支援日期時間資料類型的資料庫。  
  
下表摘要了可以在 [查詢和檢視設計師] 不同窗格中使用的各種日期格式。  
  
|**窗格**|**日期格式**|  
|------------|-------------------|  
|準則|地區設定特性 資料庫特性 ANSI 標準<br /><br />在 [準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) 中輸入的日期，會在 SQL 窗格中轉換為與資料庫相容的格式。|  
|SQL|資料庫特性 ANSI 標準|  
|結果|地區設定特性|  
  
## <a name="searching-on-logical-values"></a>搜尋邏輯值  
每一種資料庫的邏輯資料格式不同。 False 值常常會儲存為零 (0)。 True 值最常儲存為 1，偶爾會儲存為 -1。 下列準則適用於在搜尋條件中輸入邏輯值時：  
  
-   若要使用零搜尋 False 值，如以下例子所示：  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 0  
    ```  
  
-   搜尋 True 值時如果不確定該使用什麼格式，可以像下面例子一樣用 1 試試看：  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 1  
    ```  
  
-   或者可以搜尋任何非零值以擴大搜尋範圍，如以下例子所示：  
  
    ```  
    SELECT * FROM authors  
    WHERE contract <> 0  
    ```  
  
## <a name="see-also"></a>另請參閱  
[指定搜尋準則 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

