---
title: 選擇 - SQL 指令 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640189a5a31d0c21642b037e906bd6361690a9a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300938"
---
# <a name="select---sql-command"></a>SELECT - SQL 命令
從一個或多個表檢索數據。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的本機 Visual FoxPro 語言文法。 有關特定於驅動程式的資訊,請參閱**驅動程式備註**。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
...]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>引數  
  
> [!NOTE]  
>  *子查詢*(在以下參數中引用)是 SELECT 中的 SELECT,必須包含在括弧中。 在 WHERE 子句中,可以在同一級別(未嵌套)最多具有兩個子查詢。 (請參閱參數的該部分。子查詢可以包含多個聯接條件。  
  
 [所有&#124;  [*別名*].*Select_Item* [as *Column_Name*] [ , [*別名*. ]*Select_Item* [as *Column_Name*]  
 SELECT 子句指定查詢結果中顯示的欄位、常量和運算式。  
  
 預設情況下,ALL 顯示查詢結果中的所有行。  
  
 從查詢結果中排除任何行的重複項。  
  
> [!NOTE]  
>  每個 SELECT 子句只能使用一次"  
  
 *別名*. 限定匹配項名稱。 使用*Select_Item*指定的每個項目都會生成查詢結果的一列。 如果兩個或多個項具有相同的名稱,請包括表別名和項名稱前的句點,以防止重複列。  
  
 *Select_Item*指定要包含在查詢結果中的項。 項可以是以下項目之一:  
  
-   FROM 子句表中表中的欄位的名稱。  
  
-   指定相同的常量值的常量值將顯示在查詢結果的每一行中。  
  
-   可以是使用者定義的函數名稱的運算式。  
  
 **具有 SELECT 的使用者定義函數**  
  
 儘管在 SELECT 子句中使用使用者定義的函數有明顯的好處,但您還應考慮以下限制:  
  
-   使用 SELECT 執行的操作速度可能受執行此類使用者定義的函數的速度的限制。 通過使用用 C 或彙編語言編寫的 API 和使用者定義的函數,可以更好地完成涉及使用者定義函數的高容量操作。  
  
-   將值傳遞給從 SELECT 呼叫的使用者定義的函數的唯一可靠方法是在調用函數時傳遞給該函數的參數清單。  
  
-   即使您試驗並發現一個據稱被禁止的操作,在 FoxPro 的特定版本中工作正常,也不能保證它將繼續在更高版本中工作。  
  
 除了這些限制之外,選擇子句中可以接受使用者定義的函數。 但是,請記住,使用 SELECT 可能會降低性能。  
  
 以下欄位函數可用於所列欄位的欄位或表示式的選擇項目:  
  
-   *AVG(Select_Item*)-平均一列數字數據。  
  
-   *COUNT(Select_Item*)- 計算列選擇的數量。 COUNT(*) 計算查詢輸出中的行數。  
  
-   *MIN(Select_Item*)-確定列中*Select_Item*的最小值。  
  
-   *MAX(Select_Item*)-確定列中*Select_Item*的最大值。  
  
-   *SUM(Select_Item*)-總計一列數值數據。  
  
 不能嵌套欄位函數。  
  
 如*Column_Name*  
 指定查詢輸出中列的標題。 當*Select_Item*是表達式或包含欄位函數並且您希望為列指定有意義的名稱時,這非常有用。 *Column_Name*可以是表達式,但不能包含表欄位名稱中不允許的字元(例如空格)。  
  
 從資料庫*名稱*。*表*[*Local_Alias*] [ ] [ [*資料庫名稱*! ]*表*[*Local_Alias*]  
 列出包含查詢檢索數據的表。 如果沒有打開任何表,Visual FoxPro 將顯示 **「打開**」對話框,以便您可以指定檔案位置。 打開后,該表在查詢完成後保持打開狀態。  
  
 *資料庫名稱*! 指定資料庫的名稱,而不是使用資料來源指定的資料庫。 如果未使用數據源指定資料庫,則必須包含包含表的資料庫的名稱。 包括資料庫名稱後和表名稱之前的感嘆號 (!) 分隔符。  
  
 *Local_Alias*指定*表*中指定的表的臨時名稱。 如果指定本地別名,則必須在整個 SELECT 語句中使用本地別名而不是表名。 本地別名不會影響 Visual FoxPro 環境。  
  
 WHERE*加入條件*[和*加入條件*...]   [和&#124;或*篩選條件*[和&#124; 或*篩選條件*...]  
 告訴 Visual FoxPro 在查詢結果中僅包含某些記錄。 從多個表中檢索數據需要 WHERE。  
  
 *Join條件*指定連結 FROM 子句中表的欄位。 如果在查詢中包含多個表,則應為第一個表之後的每個表指定聯接條件。  
  
> [!IMPORTANT]  
>  建立聯結條件時請考慮以下資訊:  
  
-   如果在查詢中包含兩個表,並且未指定聯接條件,則只要滿足篩選器條件,第一個表中的每個記錄都將聯接到第二個表中的每個記錄。 此類查詢可以產生冗長的結果。  
  
-   將表與空欄位聯接時要小心,因為 Visual FoxPro 匹配空欄位。 例如,如果您加入 CUSTOMER。郵編和發票。ZIP,如果 CUSTOMER 包含 100 個空郵政編碼,並且 INVOICE 包含 400 個空郵遞區編碼,則查詢輸出包含由空欄位產生的額外記錄 40,000 條。 使用**EMPTY( 函數**從查詢輸出中消除空記錄)。  
  
-   您必須使用 AND 運算子連接多個聯接條件。 每個聯結條件都有以下形式:  
  
     *欄位名稱1 比較欄位名稱2*  
  
     *FieldName1*是表格中的欄位的名稱 *,FieldName2*是另一個表中的欄位的名稱,*比較*是下表中描述的運算元之一。  
  
|運算子|比較|  
|--------------|----------------|  
|=|等於|  
|==|完全相等|  
|LIKE|SQL 喜歡|  
|<>,!,##|不等於|  
|>|超過|  
|>=|超過或等於|  
|<|小於|  
|<=|小於或等於|  
  
 使用帶有字串的 + 運算元時,它的作用會有所不同,具體取決於 SET ANSI 的設置。 當 SET ANSI 設定為 OFF 時,Visual FoxPro 會以 Xbase 使用者熟悉的方式處理字串比較。 當 SET ANSI 設定為 ON 時,Visual FoxPro 遵循用於字串比較的 ANSI 標準。 有關 Visual FoxPro 如何執行字串比較的詳細資訊,請參閱[SET ANSI](../../odbc/microsoft/set-ansi-command.md)和[SET EXACT。](../../odbc/microsoft/set-exact-command.md)  
  
 *篩選器條件*指定記錄必須滿足的條件才能包含在查詢結果中。 您可以在查詢中根據需要包含盡可能多的篩選器條件,將它們與 AND 或 OR 運算子連接。 您還可以使用 NOT 運算子反轉邏輯表示式的值,也可以使用**EMPTY( )** 檢查空欄位。 *篩選器條件*可以採用以下範例中的任何表單:  
  
 **範例 1** *欄位名稱 1 位元名稱2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **範例 2** *欄位名稱比較表示式*  
  
 `payments.amount >= 1000`  
  
 **範例 3** *欄位名稱比較*全部 (*子查詢*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 當篩選器條件包含 ALL 時,該欄位必須滿足子查詢生成的所有值的比較條件,然後才能將其記錄包含在查詢結果中。  
  
 **範例 4** *字段名稱比較*任何&#124; A(*子查詢*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 當篩選器條件包括 ANY 或 SOME 時,該欄位必須滿足子查詢生成的至少一個值的比較條件。  
  
 以下範例檢查欄位中的值是否在指定的值範圍內:  
  
 **範例 5***欄位名稱*[不是] *Start_Range*與*End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 下面的示例檢查至少一行是否符合子查詢中的條件。 當篩選器條件包括 EXISTS 時,篩選器條件將評估為 True (。T.),除非子查詢計算為空集。  
  
 **範例 6** [NOT] 存在 (*子查詢*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **範例 7** *字段名稱*[不] *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 當篩選器條件包含 IN 時,該欄位必須包含其中一個值,然後才能將其記錄包含在查詢結果中。  
  
 **範例 8** *欄位名稱*[NOT] IN (*子查詢*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 此處,該欄位必須包含子查詢返回的值之一,然後才能將其記錄包含在查詢結果中。  
  
 **範例 9** *欄位名稱*[NOT] 喜歡*c 運算式*  
  
 `customer.country NOT LIKE "USA"`  
  
 此篩選器條件搜索與*cExpression*匹配的每個欄位。 您可以使用百分比符號 (%)和下劃線( + ) 通配符作為*cExpression*的一部分。 下劃線表示字串中的單個未知字元。  
  
 群組 BY*群組列*[,*群組欄*...  
 根據一個或多個列中的值對查詢中的行進行分組。 *群組列*可以是以下之一:  
  
-   常規表欄位的名稱。  
  
-   包含 SQL 欄位函數的欄位。  
  
-   指示結果表中列位置的數字表達式。 (最左邊的列號為 1。  
  
 有*篩選準則*  
 指定組必須滿足的篩選器條件才能包含在查詢結果中。 在 GROUP BY 中應使用,並且可以根據需要包含盡可能多的篩選器條件,由 AND 或 OR 運算子連接。 您還可以使用 NOT 來反轉邏輯表達式的值。  
  
 *篩選器條件*不能包含子查詢。  
  
 沒有 GROUP BY 子句的"一條"問題子項的行為類似於 WHERE 子句。 您可以在「有」子句中使用本地別名和欄位函數。 如果您的"有內容"子句不包含欄位函數,請使用 WHERE 子句來提高性能。  
  
 [聯合 [所有]*選擇指令*|  
 將一個 SELECT 的最終結果與另一個 SELECT 的最終結果相結合。 默認情況下,UNION 會檢查組合的結果並消除重複的行。 使用括弧組合多個 UNION 子句。  
  
 ALL 可防止 UNION 從組合結果中消除重複行。  
  
 UNION 條款遵循以下規則:  
  
-   不能使用 UNION 組合子查詢。  
  
-   兩個 SELECT 命令的查詢輸出中必須具有相同的列數。  
  
-   一個 SELECT 查詢結果中的每個列必須具有與其他 SELECT 中的相應列相同的數據類型和寬度。  
  
-   只有最終 SELECT 可以具有 ORDER BY 子句,該子句必須按數位引用輸出列。 如果包含 ORDER BY 子句,則會影響完整結果。  
  
 您還可以使用 UNION 子句來類比外部聯接。  
  
 在查詢中聯接兩個表時,輸出中僅包含具有匹配值的記錄。 如果父表中的記錄在子表中沒有相應的記錄,則父表中的記錄不包括在輸出中。 外部聯接允許您在輸出中包括父表中的所有記錄以及子表中的匹配記錄。 要在 Visual FoxPro 中建立外部聯接,必須使用巢狀使用者 SELECT 命令,如以下範例所示:  
  
```  
SELECT customer.company, orders.order_id, orders.emp_id ;  
FROM customer, orders ;  
WHERE customer.cust_id = orders.cust_id ;  
UNION ;  
SELECT customer.company, 0, 0 ;  
FROM customer ;  
WHERE customer.cust_id NOT IN ;  
(SELECT orders.cust_id FROM orders)  
```  
  
> [!NOTE]  
>  請確保包含每個分號之前緊鄰的空間。 否則,您將收到錯誤。  
  
 UNION 子句之前的命令部分從具有匹配值的兩個表中選擇記錄。 不包括沒有關聯發票的客戶公司。 UNION 子句之後的命令部分選擇客戶表中在訂單表中沒有匹配記錄的記錄。  
  
 關於命令的第二部分,請注意以下內容:  
  
-   首先處理括弧內的 SELECT 語句。 此語句創建訂單表中所有客戶編號的選擇。  
  
-   WHERE 子句查找客戶表中未在訂單表中的所有客戶編號。 由於命令的第一部分提供了訂單表中具有客戶編號的所有公司,因此客戶表中的所有公司現在都包含在查詢結果中。  
  
-   由於 UNION 中包含的表的結構必須相同,因此第二個 SELECT 語句中有兩個占位符來表示*訂單.order_id*和*訂單.emp_id*來自第一個 SELECT 語句。  
  
    > [!NOTE]  
    >  占位元的類型必須與它們表示的欄位相同。 如果欄位是日期類型,則佔位元應為 * / * 。 如果欄位是字元欄位,則占位元應為空字串 ("")。  
  
 Order_Item *[ASC* &#124; DESC] *[Order_Item* [ASC &#124; DESC]  
 根據一個或多個列中的數據對查詢結果進行排序。 每個*Order_Item*必須對應於查詢結果中的列,可以是以下項之一:  
  
-   FROM 表中的欄位,也是主 SELECT 子句中的選定項(不在子查詢中)。  
  
-   指示結果表中列位置的數字表達式。 (最左邊的列是第 1 號。  
  
 ASC 根據訂單項或項指定查詢結果的提升順序,是 ORDER BY 的預設值。  
  
 DESC 為查詢結果指定降序。  
  
 如果不使用 ORDER BY 指定訂單,則查詢結果將無序顯示。  
  
## <a name="remarks"></a>備註  
 SELECT 是一個 SQL 命令,與任何其他 Visual FoxPro 命令一樣內建於 Visual FoxPro 中。 當您使用 SELECT 進行查詢時,Visual FoxPro 會解釋查詢並從表中檢索指定的數據。 您可以從命令提示視窗或 Visual FoxPro 程式(與任何其他 Visual FoxPro 命令一樣)創建 SELECT 查詢。  
  
> [!NOTE]  
>  SELECT 不尊重使用 SET FILTER 指定的當前篩選器條件。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句 SELECT 發送到資料來源時,Visual FoxPro ODBC 驅動程式將該命令轉換為 Visual FoxPro SELECT 命令,無需翻譯,除非該命令包含 ODBC 轉義序列。 ODBC 轉義序列中包含的專案將轉換為 Visual FoxPro 語法。 有關使用 ODBC 逸出序列的詳細資訊,請參閱[時間和日期函數](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md), 以及 Microsoft *ODBC 程式的參考*,請參閱[ODBC 中的轉義序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立表 - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [插入 - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [設定精確](../../odbc/microsoft/set-exact-command.md)
