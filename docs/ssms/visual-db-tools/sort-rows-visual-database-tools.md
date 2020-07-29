---
title: 排序資料列
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- sorting rows [SQL Server]
- sorting query results [SQL Server]
ms.assetid: 780ef467-f96e-4373-8235-6dacbedb05a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: d7d7409f6f52c7fa178eb276f6878d22854d0157
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999325"
---
# <a name="sort-rows-visual-database-tools"></a>排序資料列 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
您可以排列查詢結果中的資料列。 也就是說，您可以命名特定的資料行或資料行組合，其值將決定結果集中的資料列排列順序。  
  
> [!NOTE]  
> 排序次序一部份取決於資料行的定序序列。 您可以在 [定序對話方塊](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md)中變更定序序列。  
  
您可以使用以下幾種方法來排序查詢結果：  
  
-   **您可以使用遞增或遞減順序來排列資料列** ：根據預設值，SQL 會使用資料行排序依據以遞增方式排列資料列。 例如，若要使用遞減價格來排列書名，只要在價格資料行中排序資料列即可。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price  
    ```  
  
    另一方面，若要先排列較昂貴的書籍名稱，您可以明確的指定使用先排列最貴的書籍的排列順序。 也就是說，您可以指定在價格資料行使用遞減值的方式來排列結果資料列。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **您可以依多重資料行排序** ：例如，您可以建立結果集，其中一個資料列列出所有作者，並先使用州來排序，然後再使用城市來排序。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT *  
    FROM authors   
    ORDER BY state, city  
    ```  
  
-   **您可以依不在結果集顯示的資料行排序** ：例如，您可以建立結果集並先列出昂貴的書籍，即使該結果集中並未顯示價格。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT title_id, title  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **您可以依衍生資料行排序**：例如，您可以建立結果集，其中每個資料列都含有書名；需付較高版稅的書將優先顯示。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT title, price * royalty / 100 as royalty_per_unit  
    FROM titles  
    ORDER BY royalty_per_unit DESC  
    ```  
  
    (強調顯示的文字部份為計算每本書所賺取的版稅公式)。  
  
    若要計算衍生的資料行，您可以如同前述的範例使用 SQL 語法，或者使用會傳回數值類值的使用者定義函數。 如需使用者定義函數的詳細資訊，請參閱 SQL Server 文件。  
  
-   **您可以排序群組資料列**：例如，您可以建立結果集，其中每個資料列描述某個城市，以及該城市中的作者數目；包含多位作者的城市將優先顯示。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ORDER BY COUNT(*) DESC, state  
    ```  
  
    注意，查詢會使用 `state` 做為次要排序資料行。 因此，如果有兩個州擁有相同數量的作者，該州將以字母順序排列。  
  
-   **您可以使用國際資料排序** ：也就是說，您可以使用定序慣例來排序資料行，這種定序慣例與該資料行的預設慣例不同。 例如，您可以撰寫擷取所有由 Jaime Patiño 所著書籍名稱的查詢。 若要以字母順序顯示名稱，您可以使用西班牙文定序序列來排列名稱資料行。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT title  
    FROM   
        authors   
        INNER JOIN   
            titleauthor   
            ON authors.au_id   
            =  titleauthor.au_id   
            INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
    WHERE   
         au_fname = 'Jaime' AND   
         au_lname = 'Patiño'  
    ORDER BY   
         title COLLATE SQL_Spanish_Pref_CP1_CI_AS  
    ```  
  
## <a name="see-also"></a>另請參閱  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
