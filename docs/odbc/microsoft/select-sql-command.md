---
title: 選取的 SQL 命令 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e7295a800b3cc84f6eb64f5dfa762573fe80b6b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="select---sql-command"></a>選取的 SQL 命令
從一或多個資料表中擷取資料。  
  
 Visual FoxPro ODBC 驅動程式支援的原生 Visual FoxPro 語言語法，此命令。 驅動程式特定資訊，請參閱**驅動程式註解**。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
…]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>引數  
  
> [!NOTE]  
>  A*子查詢*、 下列引數所指、 SELECT 中是選取和必須括在括號。 您可以在相同層級最多兩個的子查詢 （不在巢狀） 的 WHERE 子句中。 （請參閱該區段的引數）。子查詢可以包含多個聯結條件。  
  
 [所有 &#124;相異] [*別名*。]*Select_Item* [AS *Column_Name*] [，[*別名*。]*Select_Item* [AS *Column_Name*]...]  
 SELECT 子句會指定欄位、 常數和查詢結果中顯示的運算式。  
  
 根據預設，所有查詢結果中顯示了所有資料列。  
  
 DISTINCT 查詢結果中排除任何資料列的重複項的目。  
  
> [!NOTE]  
>  您可以使用 DISTINCT 一次，每個選取的子句。  
  
 *別名*。 限定相符的項目名稱。 您指定與每個項目*Select_Item*產生查詢結果的一個資料行。 如果兩個或多個項目有相同的名稱，包括資料表別名和項目名稱，以防止被複製的資料行之前的期間。  
  
 *Select_Item*指定要包含在查詢結果中的項目。 項目可以是下列其中一項：  
  
-   從 FROM 子句中資料表的欄位名稱。  
  
-   常數，指定相同的常數值會出現在查詢結果的每個資料列。  
  
-   運算式，可以是使用者定義函式的名稱。  
  
 **與選取的使用者定義函數**  
  
 雖然在 SELECT 子句中使用使用者定義函數有明顯的好處，您也應該考慮下列限制：  
  
-   執行與選取之作業的速度可能會受限於這類使用者定義函式會執行的速度。 包含使用者定義函數的大量的操作可能會更好可藉由使用 API 和 C 或組件語言撰寫的使用者定義函數。  
  
-   將值傳遞到叫用從選取的使用者定義函式的唯一可靠方式是叫用時傳遞至函數的引數清單。  
  
-   即使您實驗及探索 FoxPro 版中正常運作的真地禁止的操作時，沒有保證它將繼續在更新版本中運作。  
  
 除了這些限制，使用者定義函式是 SELECT 子句中可接受的。 不過，請記得使用 SELECT 可能會降低效能。  
  
 下列欄位函式可供使用與選取的項目是欄位或牽涉到欄位的運算式：  
  
-   AVG (*Select_Item*) — 計算平均值的數值資料的資料行。  
  
-   計數 (*Select_Item*) — 計算的資料行中的選取項目數目。 COUNT(*) 計算查詢輸出中的資料列數目。  
  
-   MIN (*Select_Item*)-最小的值會決定*Select_Item*資料行中。  
  
-   最大值 (*Select_Item*) — 最大的值會決定*Select_Item*資料行中。  
  
-   SUM (*Select_Item*) — 總計數值的資料行。  
  
 您無法巢狀欄位函式。  
  
 AS *Column_Name*  
 在查詢輸出中指定資料行標題。 這非常有用時*Select_Item*是運算式，或包含欄位函式，而且您想要提供資料行有意義的名稱。 *Column_Name*可以是運算式，但不能包含資料表的欄位名稱中不允許的字元 （例如，空格）。  
  
 從 [*DatabaseName*！]*資料表*[*Local_Alias*] [，[*DatabaseName*！]*資料表*[*Local_Alias*]...]  
 列出包含查詢所擷取之資料的資料表。 如果沒有資料表開啟時，就會顯示 Visual FoxPro**開啟**對話方塊，讓您指定的檔案位置。 已開啟之後，資料表會保持開啟，查詢完成後。  
  
 *DatabaseName*！ 指定與資料來源所指定以外的資料庫名稱。 您必須包含的資料庫包含的資料表，如果未指定資料庫與資料來源的名稱。 在資料庫名稱之後和資料表名稱前面包含驚嘆號 （！） 分隔符號。  
  
 *Local_Alias*指定資料表中的暫存名稱*資料表*。 如果您指定本機的別名，您必須使用本機的別名，而非整個 SELECT 陳述式的資料表名稱。 本機的別名不會影響 Visual FoxPro 環境。  
  
 其中*JoinCondition* [AND *JoinCondition* ...]   [和 &#124;或者*FilterCondition* [AND &#124;或者*FilterCondition* ...]]  
 告知 Visual FoxPro 查詢結果中包含特定的記錄。 視需要從多個資料表擷取資料。  
  
 *JoinCondition*指定連結在 FROM 子句中的資料表的欄位。 如果您在查詢中包含多個資料表，您應該指定每個資料表的聯結條件，第一個之後。  
  
> [!IMPORTANT]  
>  當您建立的聯結條件時，請考慮下列資訊：  
  
-   如果您在查詢中包含兩個資料表，而且未指定聯結條件，第一個資料表中的每一筆記錄會加入第二個資料表中的每一筆記錄，只要符合篩選條件。 這類查詢會產生執行時間較長的結果。  
  
-   當聯結資料表的空白欄位，因為 Visual FoxPro 符合空白欄位，請務必小心。 例如，如果您加入 CUSTOMER 上。ZIP 及發票。壓縮，並在查詢輸出如果客戶包含 100 空的郵遞區號，發票包含 400 空的郵遞區號包含 40,000 所得到的空白欄位的額外記錄。 使用**空的 （)**消除空記錄從查詢輸出的函式。  
  
-   您必須使用 AND 運算子來連接多個聯結條件。 每個 join 條件具有下列格式：  
  
     *FieldName1 比較 FieldName2*  
  
     *FieldName1*是從一個資料表中，欄位名稱*FieldName2*是從另一個資料表中，欄位的名稱和*比較*是其中一個運算子，如下表所示。  
  
|運算子|比較|  
|--------------|----------------|  
|=|等於|  
|==|完全等於|  
|LIKE|類似 SQL|  
|<>, !=, #|不等於|  
|>|多個|  
|>=|大於或等於|  
|<|小於|  
|<=|小於或等於|  
  
 當您使用 = 運算子與字串，其運作方式會不同，根據設定的 ANSI 設定。 當設定 ANSI 設定為 OFF 時，Visual FoxPro Xbase 使用者熟悉的方式處理字串比較。 當設定 ANSI 設定設為 ON 時，Visual FoxPro 遵循 ANSI 標準的字串比較。 請參閱[設定 ANSI](../../odbc/microsoft/set-ansi-command.md)和[確切設定](../../odbc/microsoft/set-exact-command.md)如需有關 Visual FoxPro 執行字串比較的方式。  
  
 *FilterCondition*指定記錄必須符合包含在查詢結果的準則。 您可以包含篩選條件查詢中的所要使用 AND 或 OR 運算子。 您也可以使用 NOT 運算子，若要反轉的邏輯運算式的值，或者您可以使用**空的 （)**檢查的空白欄位。 *FilterCondition*可能需要在下列範例中任何一種格式：  
  
 **範例 1** *FieldName1 比較 FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **範例 2** *FieldName 比較運算式*  
  
 `payments.amount >= 1000`  
  
 **範例 3** *FieldName 比較*所有 (*子查詢*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 當篩選條件包含所有時，欄位必須符合其記錄包含在查詢結果之前，子查詢所產生的所有值的比較條件。  
  
 **範例 4** *FieldName 比較*任何 &#124;某些 (*子查詢*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 當篩選條件會包含下列任何或部分時，此欄位必須符合至少其中一個子查詢所產生的值的比較條件。  
  
 下列範例會檢查以查看欄位中的值是否在指定的值範圍內：  
  
 **範例 5** *FieldName* [NOT] 之間*Start_Range* AND *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 下列範例會檢查是否至少一個資料列符合子查詢中的準則。 當篩選條件包含 EXISTS 時，篩選條件評估為 True (。T.) 除非子查詢會評估為空集合。  
  
 **範例 6** [NOT] 是否存在 (*子查詢*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **範例 7** *FieldName* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 當篩選條件包含中時，此欄位必須包含其中一個值之前的記錄包含在查詢結果。  
  
 **範例 8** *FieldName* [NOT] IN (*子查詢*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 在此欄位必須包含其中一個子查詢傳回查詢結果中包含的記錄之前的值。  
  
 **範例 9** *FieldName* [NOT] LIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 此篩選條件會搜尋比對每個欄位*cExpression*。 您可以使用百分比符號 （%） 和底線 (_) 萬用字元所組成，一部分*cExpression*。 底線表示未知的單一字元，在字串中。  
  
 GROUP BY *GroupColumn* [， *GroupColumn* ...]  
 一或多個資料行中值為基礎的查詢中的群組資料列。 *GroupColumn*可以是下列其中之一：  
  
-   一般表格欄位的名稱。  
  
-   包含 SQL 欄位函式的欄位。  
  
-   數值運算式，指出資料行的結果資料表中的位置。 （最左邊資料行數目是 1）。  
  
 具有*FilterCondition*  
 指定群組時必須符合包含在查詢結果的篩選條件。 HAVING 應搭配 GROUP BY，而且可以包含篩選條件所要連接 AND 或 OR 運算子。 您也可以使用不到邏輯運算式的值。  
  
 *FilterCondition*不能包含子查詢。  
  
 HAVING 子句不含 GROUP BY 子句的行為類似 WHERE 子句。 您可以使用本機的別名和欄位函式的 HAVING 子句。 使用 WHERE 子句，藉以改善效能，如果 HAVING 子句中不包含任何欄位函式。  
  
 [聯集 [ALL] *SELECTCommand*]  
 使用另一個選取的最終結果結合一個選取的最終結果。 根據預設，UNION 檢查合併的結果，並消除重複的資料列。 您可以使用括號來結合多個 UNION 子句。  
  
 所有可防止聯集消除重複的資料列之組合結果中。  
  
 UNION 子句會遵循下列規則：  
  
-   您無法使用 UNION 來合併子查詢。  
  
-   這兩個選取的命令必須在其查詢輸出中有相同數目的資料行。  
  
-   在其他選取的對應資料行一個選取的查詢結果中的每個資料行必須有相同的資料類型和寬度。  
  
-   最終的 SELECT 都可以有 ORDER BY 子句，它必須參考輸出資料行數。 如果包含 ORDER BY 子句，則它會影響完整的結果。  
  
 您也可以使用 UNION 子句，以模擬外部聯結。  
  
 當您在查詢中加入兩個資料表時，只有在聯結欄位相符的值與記錄會包含在輸出中。 如果父資料表中的記錄子資料表中沒有對應的記錄，父資料表中的記錄不會包含在輸出中。 外部聯結可讓您在輸出中，子資料表中相符的記錄與父資料表中包含的所有記錄。 若要建立外部聯結 Visual FoxPro，您必須使用巢狀 SELECT 命令，如下列範例所示：  
  
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
>  請確定您包含每一個分號前面的空間。 否則，您會收到錯誤。  
  
 有相符的值的命令之前 UNION 子句會從這兩個資料表中選取記錄 > 一節。 不包含客戶的公司沒有相關聯的發票。 UNION 子句之後的區段會選取 customer 資料表中沒有相符的 orders 資料表中的記錄中的記錄。  
  
 關於命令的第二個區段，請注意下列各項：  
  
-   括號內的 SELECT 陳述式會處理第一次。 這個陳述式會建立 orders 資料表中選取的所有客戶編號。  
  
-   WHERE 子句不在 「 訂單 」 資料表中的 customer 資料表中尋找所有客戶編號。 因為命令的第一個區段提供有客戶編號 orders 資料表中的所有公司，customer 資料表中的所有公司現在都包含查詢結果中。  
  
-   表示第二個 SELECT 陳述式中的等位中所包含的資料表結構必須相同，因為有兩個預留位置*orders.order_id*和*orders.emp_id*從第一個 SELECT陳述式。  
  
    > [!NOTE]  
    >  預留位置必須是相同的型別所代表的欄位。 如果欄位是日期類型，應該是預留位置 {/ /}。 如果欄位是一個字元欄位，將預留位置應該是空字串 ("")。  
  
 ORDER BY *Order_Item* [ASC &#124;DESC] [， *Order_Item* [ASC &#124;DESC]...]  
 排序查詢結果根據一個或多個資料行中的資料。 每個*Order_Item*必須對應到查詢結果中的資料行，而且可以是下列其中之一：  
  
-   也是主要的 SELECT 子句 （不在子查詢） 中的選取項目從資料表中的欄位。  
  
-   數值運算式，指出資料行的結果資料表中的位置。 (最左邊的資料行是一個數字 1。)  
  
 ASC 指定查詢結果，根據訂單項目或項目，以遞增的順序，並為 ORDER BY 的預設值。  
  
 DESC 指定查詢結果的遞減順序。  
  
 如果您未使用 ORDER BY 指定順序，會出現未排序查詢結果。  
  
## <a name="remarks"></a>備註  
 選取是內建於 Visual FoxPro 像任何其他 Visual FoxPro 命令的 SQL 命令。 當您使用會造成查詢選取，Visual FoxPro 解譯的查詢，並從資料表擷取指定的資料。 您可以建立從命令提示字元視窗或 Visual FoxPro 程式內的 SELECT 查詢 （如同任何其他 Visual FoxPro 命令）。  
  
> [!NOTE]  
>  選取不會遵守目前設定篩選器與指定的篩選條件。  
  
## <a name="driver-remarks"></a>驅動程式註解  
 當您的應用程式會將 ODBC SQL 陳述式選取傳送至資料來源時，Visual FoxPro ODBC 驅動程式會將命令轉換 Visual FoxPro 選取命令，而不需轉譯除非命令包含 ODBC 逸出序列。 ODBC 逸出序列內的項目會轉換成 Visual FoxPro 語法。 如需有關使用 ODBC 逸出序列，請參閱[時間和日期函數](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md)和*Microsoft ODBC 程式設計人員參考*，請參閱[ODBC 中的逸出序列](../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
## <a name="see-also"></a>請參閱  
 [建立資料表-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [插入-SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [設定正確](../../odbc/microsoft/set-exact-command.md)
