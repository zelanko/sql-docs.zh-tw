---
title: 建立查詢使用除了資料表的項目 (Visual Database Tools) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], queries
- queries [SQL Server], creating
ms.assetid: 8e4a1f0a-8a42-4733-be8d-e21d6dbddb33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6cd83135da7e5c9f4dac9e41ff562551d14ab20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63184329"
---
# <a name="create-queries-using-something-besides-a-table-visual-database-tools"></a>使用資料表以外的項目建立查詢 (Visual Database Tools)
  當您編寫擷取查詢時，應該明白指出您要的資料行、您要的資料列和查詢處理器尋找原始資料的位置。 通常其原始資料是由某資料表組成或由數個資料表聯結在一起。 但原始資料可能源自資料表以外的來源。 其實，原始資料可以來自檢視、查詢、同義資料表或傳回資料表的使用者定義函數。  
  
## <a name="using-a-view-in-place-of-a-table"></a>使用檢視取代資料表  
 您可以選取檢視的資料列。 例如，假設資料庫中含有名為「ExpensiveBooks」的檢視，其中每個資料列將說明價錢超過 19.99 的書名。 其檢視定義將如下所示：  
  
```  
SELECT *  
FROM titles  
WHERE price > 19.99  
  
```  
  
 只要選取 [ExpensiveBooks] 檢視中的心理書籍，您就可以選取昂貴的心理書籍。 產生的 SQL 將如下所示：  
  
```  
SELECT *  
FROM ExpensiveBooks  
WHERE type = 'psychology'  
  
```  
  
 同樣的，JOIN 作業中也可以使用檢視。 例如，只要將銷售資料表聯結至 [ExpensiveBooks] 檢視，您就可以尋找昂貴書籍的銷售量。 產生的 SQL 將如下所示：  
  
```  
SELECT *  
FROM sales   
         INNER JOIN   
         ExpensiveBooks   
         ON sales.title_id   
         =  ExpensiveBooks.title_id  
  
```  
  
 如需新增檢視至查詢的詳細資訊，請參閱[將資料表新增至查詢 &#40;Visual Database Tools&#41;](visual-database-tools.md)。  
  
## <a name="using-a-query-in-place-of-a-table"></a>使用查詢取代資料表  
 您可以選取查詢中的資料列。 例如，假設您已撰寫某查詢來擷取合著書籍 (具有一位以上作者的書籍) 的書名和識別碼。 產生的 SQL 將如下所示：  
  
```  
SELECT   
     titles.title_id, title, type  
FROM   
     titleauthor   
         INNER JOIN  
         titles   
         ON titleauthor.title_id   
         =  titles.title_id   
GROUP BY   
     titles.title_id, title, type  
HAVING COUNT(*) > 1  
  
```  
  
 您可以再編寫其他查詢來建置該結果。 例如，您可以編寫擷取由多位作者合著的心理書籍之查詢。 若要編寫此新查詢，您可以使用現有查詢做為新查詢資料的來源。 產生的 SQL 將如下所示：  
  
```  
SELECT   
    title  
FROM   
    (  
    SELECT   
        titles.title_id,   
        title,   
        type  
    FROM   
        titleauthor   
            INNER JOIN  
            titles   
            ON titleauthor.title_id   
            =  titles.title_id   
    GROUP BY   
        titles.title_id,   
        title,   
        type  
    HAVING COUNT(*) > 1  
    )   
    co_authored_books  
WHERE     type = 'psychology'  
  
```  
  
 加強顯示的文字表示做為新查詢資料來源的現有查詢。 請注意新的查詢使用別名 (「co_authored_books」) 來稱呼現有查詢。 如需別名的詳細資訊，請參閱[建立資料表別名 &#40;Visual Database Tools&#41;](create-table-aliases-visual-database-tools.md) 和[建立資料行別名 &#40;Visual Database Tools&#41;](create-column-aliases-visual-database-tools.md)。  
  
 同樣的，JOIN 作業中可使用查詢。 例如，只要將 [ExpensiveBooks] 檢視聯結至擷取由多位作者合著的書籍的查詢，您便可以尋找昂貴的合著書籍之銷售。 產生的 SQL 將如下所示：  
  
```  
SELECT   
    ExpensiveBooks.title  
FROM   
    ExpensiveBooks   
        INNER JOIN  
        (  
        SELECT   
            titles.title_id,   
            title,   
            type  
        FROM   
            titleauthor   
                INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
        GROUP BY   
            titles.title_id,   
            title,   
            type  
        HAVING COUNT(*) > 1  
        )  
```  
  
 如需新增查詢至查詢的詳細資訊，請參閱[將資料表新增至查詢 &#40;Visual Database Tools&#41;](visual-database-tools.md)。  
  
## <a name="using-a-user-defined-function-in-place-of-a-table"></a>使用使用者定義函數取代資料表  
 在 SQL Server 2000 (含) 以上版本中，您可以建立可傳回資料表的使用者定義函數。 執行複雜或程序邏輯時，這類函數便非常有用。  
  
 例如，假設員工資料表含有額外的資料行 employee.manager_emp_id，而且外部索引鍵存在於 manager_emp_id 到 employee.emp_id 之間。 在員工資料表的每個資料列中，manager_emp_id 資料行將指出員工的上司。 更明確地說，它會指出員工上司的 emp_id。 您可以建立傳回資料表的使用者定義函數，其中該資料表將包含一資料列列出在特定職等管理人員的組織結構中工作的員工。 您可以呼叫 fn_GetWholeTeam 函式，並設計該函式採用輸入變數，即管理人員 (您想要擷取該管理人員所屬小組) 的 emp_id。  
  
 您可以編寫使用 fn_GetWholeTeam 函數做為資料來源的查詢。 產生的 SQL 將如下所示：  
  
```  
SELECT *   
FROM   
     fn_GetWholeTeam ('VPA30890F')  
  
```  
  
 "VPA30890F" 是管理人員的 emp_id，您將擷取該管理人員的組織。 如需新增使用者定義函數至查詢的詳細資訊，請參閱[將資料表新增至查詢 &#40;Visual Database Tools&#41;](visual-database-tools.md)。 如需使用者定義函數的完整描述，請參閱[使用者定義函數](../../relational-databases/user-defined-functions/user-defined-functions.md)。  
  
  
