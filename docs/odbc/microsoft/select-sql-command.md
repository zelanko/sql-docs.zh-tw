---
title: SELECT-SQL 命令 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300938"
---
# <a name="select---sql-command"></a>SELECT - SQL 命令
抓取一或多個資料表中的資料。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的原生 Visual FoxPro 語言語法。 如需驅動程式特定的資訊，請參閱**驅動程式備註**。  
  
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
>  在下列引數中參考的*子查詢*是 select 內的 select，而且必須以括弧括住。 在 WHERE 子句中，您最多可以在相同層級（非嵌套）上有兩個子查詢。 （請參閱引數的那一節）。子查詢可以包含多個聯結條件。  
  
 [ALL &#124; DISTINCT]  [*Alias*.]*Select_Item* [AS *Column_Name*] [，[*Alias*.]*Select_Item* [AS *Column_Name*] ...]  
 SELECT 子句會指定要顯示在查詢結果中的欄位、常數和運算式。  
  
 根據預設，[全部] 會顯示查詢結果中的所有資料列。  
  
 DISTINCT：從查詢結果中排除任何資料列的重複專案。  
  
> [!NOTE]  
>  每個 SELECT 子句只能使用 DISTINCT 一次。  
  
 *別名*。 符合專案名稱的資格。 您使用*Select_Item*所指定的每個專案都會產生一個查詢結果的資料行。 如果有兩個或多個專案具有相同的名稱，請在專案名稱前面加上資料表別名和句點，以防止重復資料行。  
  
 *Select_Item*指定要包含在查詢結果中的專案。 專案可以是下列其中一項：  
  
-   FROM 子句中資料表的功能變數名稱。  
  
-   常數，指定相同的常數值會出現在查詢結果的每個資料列中。  
  
-   運算式，可以是使用者定義函數的名稱。  
  
 **具有 SELECT 的使用者定義函數**  
  
 雖然在 SELECT 子句中使用使用者自訂函數有明顯的好處，但您也應該考慮下列限制：  
  
-   使用 SELECT 執行之作業的速度，可能會受到這類使用者定義函數的執行速度限制。 使用以 C 或元件語言撰寫的 API 和使用者定義函式，可能會更好地完成涉及使用者定義函數的大量操作。  
  
-   將值傳遞給從 SELECT 叫用的使用者定義函數的唯一可靠方法，是在叫用時傳遞至函式的引數清單。  
  
-   即使您實驗並探索在特定版本的 FoxPro 中可正常運作的被認為禁止操作，也不保證它會繼續在較新的版本中運作。  
  
 除了這些限制外，SELECT 子句中也可接受使用者定義的函數。 不過，請記住，使用 SELECT 可能會使效能變慢。  
  
 下欄欄位函數可與屬於欄位的選取專案或涉及欄位的運算式搭配使用：  
  
-   AVG （*Select_Item*）-數值資料的資料行平均值。  
  
-   COUNT （*Select_Item*）-計算資料行中選取專案的數目。 COUNT （*）會計算查詢輸出中的資料列數目。  
  
-   MIN （*Select_Item*）-判斷資料行中*Select_Item*的最小值。  
  
-   MAX （*Select_Item*）-判斷資料行中*Select_Item*的最大值。  
  
-   SUM （*Select_Item*）-總計數值資料的資料行。  
  
 您不能嵌套欄位函數。  
  
 AS *Column_Name*  
 指定查詢輸出中的資料行標題。 當*Select_Item*是運算式或包含欄位函數，而您想要為數據行提供有意義的名稱時，這會很有用。 *Column_Name*可以是運算式，但不能包含資料表功能變數名稱中不允許的字元（例如空格）。  
  
 FROM [*DatabaseName*！]*資料表*[*Local_Alias*] [，[*DatabaseName*！]*資料表*[*Local_Alias*] ...]  
 列出包含查詢所抓取之資料的資料表。 如果未開啟任何資料表，Visual FoxPro 會顯示 [**開啟**] 對話方塊，讓您可以指定檔案位置。 開啟之後，資料表會在查詢完成後維持開啟狀態。  
  
 *DatabaseName*！ 指定與資料來源指定的資料庫名稱。 如果資料庫不是以資料來源指定，您必須包含包含資料表的資料庫名稱。 在資料庫名稱後面和資料表名稱前面加上驚嘆號（！）分隔符號。  
  
 *Local_Alias*會指定*資料表*中名為之資料表的暫存名稱。 如果您指定本機別名，則必須在整個 SELECT 語句中使用本機別名，而不是資料表名稱。 本機別名不會影響 Visual FoxPro 環境。  
  
 其中*JoinCondition* [AND *JoinCondition* ...]   [AND &#124; 或*FilterCondition* [AND &#124; or *FilterCondition* ...]]  
 告訴 Visual FoxPro 僅包含查詢結果中的特定記錄。 從多個資料表中取出資料時需要的位置。  
  
 *JoinCondition*指定連結 from 子句中資料表的欄位。 如果您在查詢中包含一個以上的資料表，您應該在第一個資料表之後指定一個聯結條件。  
  
> [!IMPORTANT]  
>  當您建立聯結條件時，請考慮下列資訊：  
  
-   如果您在查詢中包含兩個數據表，但未指定聯結條件，則只要符合篩選準則，第一個資料表中的每筆記錄就會聯結至第二個數據表中的每筆記錄。 這類查詢可能會產生冗長的結果。  
  
-   聯結具有空白欄位的資料表時，請務必小心，因為 Visual FoxPro 符合空白欄位。 例如，如果您加入 CUSTOMER。ZIP 和發票。ZIP，如果客戶包含100的空白郵遞區號，而發票包含400空的郵遞區號，則查詢輸出會包含來自空白欄位所產生的40000個額外記錄。 您可以使用**EMPTY （）** 函數來排除查詢輸出中的空白記錄。  
  
-   您必須使用 AND 運算子來連接多個聯結條件。 每個聯結條件的形式如下：  
  
     *FieldName1 比較 FieldName2*  
  
     *FieldName1*是一個資料表中的功能變數名稱， *FieldName2*是另一個資料表中的功能變數名稱，而*比較*是下表所述的其中一個運算子。  
  
|運算子|比較|  
|--------------|----------------|  
|=|等於|  
|==|完全相等|  
|LIKE|SQL LIKE|  
|<>、！ =、#|不等於|  
|>|超過|  
|>=|大於或等於|  
|<|小於|  
|<=|小於或等於|  
  
 當您搭配字串使用 = 運算子時，它的運作方式會不同，視 SET ANSI 的設定而定。 當 SET ANSI 設定為 OFF 時，Visual FoxPro 會以 Xbase 使用者熟悉的方式來處理字串比較。 當 SET ANSI 設定為 ON 時，Visual FoxPro 會遵循 ANSI 標準來進行字串比較。 如需有關 Visual FoxPro 如何執行字串比較的詳細資訊，請參閱[SET ANSI](../../odbc/microsoft/set-ansi-command.md)和[set EXACT](../../odbc/microsoft/set-exact-command.md) 。  
  
 *FilterCondition*指定記錄必須符合的條件，才能包含在查詢結果中。 您可以視需要在查詢中包含多個篩選準則，並使用 AND 或 OR 運算子加以連接。 您也可以使用 NOT 運算子來反轉邏輯運算式的值，也可以使用**empty （）** 來檢查空白欄位。 *FilterCondition*可以採用下列範例中的任何表單：  
  
 **範例 1** *FieldName1 比較 FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **範例 2** *FieldName 比較運算式*  
  
 `payments.amount >= 1000`  
  
 **範例 3** *FieldName 比較*ALL （*子查詢*）  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 當篩選準則包含 ALL 時，此欄位必須符合子查詢所產生之所有值的比較準則，才會將其記錄包含在查詢結果中。  
  
 **範例 4** *FieldName 比較*任何 &#124; SOME （*子查詢*）  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 當篩選準則包含 ANY 或 SOME 時，此欄位必須符合子查詢所產生的至少一個值的比較準則。  
  
 下列範例會檢查欄位中的值是否在指定的值範圍內：  
  
 **範例 5** *START_RANGE*和*End_Range*之間的*FieldName* [NOT]  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 下列範例會檢查是否至少有一個資料列符合子查詢中的條件。 當篩選準則包含 EXISTS 時，篩選準則會評估為 True （。T），除非子查詢評估為空的集合。  
  
 **範例 6** [不] 存在（*子查詢*）  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **範例 7**中的*FieldName* [NOT] *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 當篩選準則包含在中時，欄位必須包含其中一個值，才會將其記錄包含在查詢結果中。  
  
 **範例 8** *FieldName* [NOT] IN （*子查詢*）  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 在這裡，此欄位必須包含子查詢所傳回的其中一個值，才會將其記錄包含在查詢結果中。  
  
 **範例 9** *FieldName* [NOT] LIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 此篩選準則會搜尋符合*cExpression*的每個欄位。 您可以使用百分比符號（%）和底線（_）萬用字元做為*cExpression*的一部分。 底線代表字串中的單一未知字元。  
  
 GROUP BY *GroupColumn* [， *GroupColumn* ...]  
 根據一個或多個資料行中的值，將查詢中的資料列分組。 *GroupColumn*可以是下列其中一項：  
  
-   一般資料表欄位的名稱。  
  
-   包含 SQL 欄位函數的欄位。  
  
-   數值運算式，指出資料行在結果資料表中的位置。 （最左邊的資料行編號是1）。  
  
 具有*FilterCondition*  
 指定群組必須符合才能包含在查詢結果中的篩選準則。 HAVING 應該與 GROUP BY 搭配使用，而且可以包含您想要的多個篩選準則，並透過 AND 或 OR 運算子進行連接。 您也可以使用 NOT 來反轉邏輯運算式的值。  
  
 *FilterCondition*不能包含子查詢。  
  
 不含 GROUP BY 子句的 HAVING 子句行為就像 WHERE 子句。 您可以在 HAVING 子句中使用本機別名和欄位函數。 如果 HAVING 子句未包含任何欄位函式，請使用 WHERE 子句以提高效能。  
  
 [UNION [ALL] *SELECTCommand*]  
 結合一個 SELECT 的最後結果與另一個 SELECT 的最終結果。 根據預設，聯集會檢查合併的結果並排除重複的資料列。 使用括弧結合多個聯集子句。  
  
 ALL 會防止 UNION 從合併的結果中排除重複的資料列。  
  
 UNION 子句會遵循下列規則：  
  
-   您不能使用 UNION 來結合子查詢。  
  
-   這兩個 SELECT 命令在其查詢輸出中必須有相同數目的資料行。  
  
-   其中一個 SELECT 之查詢結果中的每個資料行，都必須與另一個 SELECT 中的對應資料行具有相同的資料類型和寬度。  
  
-   只有最後一個 SELECT 可以具有 ORDER BY 子句，這必須依數位參考輸出資料行。 如果包含 ORDER BY 子句，它會影響完整的結果。  
  
 您也可以使用 UNION 子句來模擬外部聯結。  
  
 當您在查詢中聯結兩個數據表時，輸出中只會包含具有相符值的記錄。 如果父資料表中的記錄在子資料工作表中沒有對應的記錄，則父資料表中的記錄不會包含在輸出中。 外部聯結可讓您在輸出中包含父資料表中的所有記錄，以及子資料工作表中相符的記錄。 若要在 Visual FoxPro 中建立外部聯結，您必須使用嵌套的 SELECT 命令，如下列範例所示：  
  
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
>  請確定您包含緊接在每個分號前面的空格。 否則，您將會收到錯誤。  
  
 在 UNION 子句之前，命令的區段會從兩個具有相符值的資料表中選取記錄。 沒有相關發票的客戶公司則不會包含在內。 在 UNION 子句之後，命令的區段會選取 [orders] 資料表中沒有相符記錄之 customer 資料表中的記錄。  
  
 關於命令的第二個區段，請注意下列事項：  
  
-   括弧內的 SELECT 語句會先處理。 此語句會建立 orders 資料表中所有客戶編碼的選取專案。  
  
-   WHERE 子句會在 customer 資料表中尋找不在 orders 資料表中的所有客戶編碼。 因為命令的第一個區段提供 orders 資料表中具有客戶編碼的所有公司，所以 customer 資料表中的所有公司現在都會包含在查詢結果中。  
  
-   因為等位中包含的資料表結構必須完全相同，所以第二個 SELECT 語句中有兩個預留位置代表*orders。 order_id*和*orders。 emp_id*自第一個 select 語句。  
  
    > [!NOTE]  
    >  預留位置的類型必須與它們所代表的欄位相同。 如果欄位是日期類型，則預留位置應該是 {//}。 如果欄位是字元欄位，則預留位置應該是空字串（""）。  
  
 ORDER BY *Order_Item* [ASC &#124; DESC] [， *Order_Item* [asc &#124; DESC] ...]  
 根據一或多個資料行中的資料排序查詢結果。 每個*Order_Item*都必須對應到查詢結果中的資料行，而且可以是下列其中一項：  
  
-   FROM 資料表中的欄位，也是主要 SELECT 子句中的 select 專案（不在子查詢中）。  
  
-   數值運算式，指出資料行在結果資料表中的位置。 （最左邊的資料行是數位1）。  
  
 ASC 會根據訂單專案或專案指定查詢結果的遞增順序，而且是 ORDER BY 的預設值。  
  
 DESC 指定查詢結果的遞減順序。  
  
 如果您未指定 order BY 的順序，則查詢結果會顯示為未排序。  
  
## <a name="remarks"></a>備註  
 SELECT 是 Visual FoxPro 內建的 SQL 命令，就像任何其他的 Visual FoxPro 命令一樣。 當您使用 SELECT 來提出查詢時，Visual FoxPro 會解讀查詢，並從資料表中抓取指定的資料。 您可以從 [命令提示字元] 視窗或 Visual FoxPro 程式中建立 SELECT 查詢（與任何其他 Visual FoxPro 命令一樣）。  
  
> [!NOTE]  
>  SELECT 不會遵守使用 SET FILTER 指定的目前篩選準則。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句傳送到資料來源時，Visual FoxPro ODBC 驅動程式會將命令轉換成沒有轉譯的 Visual FoxPro SELECT 命令，除非命令包含 ODBC escape 序列。 以 ODBC escape 序列括住的專案會轉換成 Visual FoxPro 語法。 如需使用 ODBC escape 序列的詳細資訊，請參閱[時間和日期](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md)函式和*Microsoft odbc 程式設計人員參考*中的「 [odbc 中的轉義順序](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)」。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT-SQL](../../odbc/microsoft/insert-sql-command.md)   
 [設定 ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [設定精確](../../odbc/microsoft/set-exact-command.md)
