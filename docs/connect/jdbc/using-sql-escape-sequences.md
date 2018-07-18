---
title: 使用 SQL 逸出序列 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 00f9e25a-088e-4ac6-aa75-43eacace8f03
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60af5198eb78ad23bf8ad55a1dc24690b91130ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852356"
---
# <a name="using-sql-escape-sequences"></a>使用 SQL 逸出序列
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支援使用 SQL 逸出序列，如 JDBC API 所定義。 逸出序列用於 SQL 陳述式，以告知驅動程式 SQL 字串的逸出部分應以不同的方式處理。 當 JDBC 驅動程式處理 SQL 字串的逸出部分時，它會將該部分的字串轉譯為 SQL Server 了解的 SQL 程式碼。  
  
 JDBC API 需要的逸出序列有五種，而且這五種都受到 JDBC 驅動程式的支援：  
  
-   LIKE 萬用字元常值  
  
-   函數處理  
  
-   日期和時間常值  
  
-   預存程序呼叫  
  
-   外部聯結  
  
-   LIMIT 逸出語法  
  
 JDBC 驅動程式所使用的逸出序列語法如下：  
  
 `{keyword ...parameters...}`  
  
> [!NOTE]  
>  JDBC 驅動程式的 SQL 逸出處理永遠保持開啟狀態。  
  
 下列幾節描述五種逸出序列，以及它們如何受到 JDBC 驅動程式支援。  
  
## <a name="like-wildcard-literals"></a>LIKE 萬用字元常值  
 JDBC 驅動程式支援`{escape 'escape character'}`使用 LIKE 子句萬用字元當做常值的語法。 例如，下列程式碼將會傳回 col3 的值，其中 col2 的值會實際以底線開頭 (而非其萬用字元用法)。  
  
```  
ResultSet rst = stmt.executeQuery("SELECT col3 FROM test1 WHERE col2   
LIKE '\\_%' {escape '\\'}");  
```  
  
> [!NOTE]  
>  逸出序列必須位於 SQL 陳述式結尾。 對於命令字串中的多個 SQL 陳述式，則逸出序列必須位於每個相關 SQL 陳述式的結尾。  
  
## <a name="function-handling"></a>函數處理  
 JDBC 驅動程式在 SQL 陳述式中支援函數逸出序列，其語法如下：  
  
```  
{fn functionName}  
```  
  
 其中`functionName`是 JDBC 驅動程式支援的函式。 例如：  
  
```  
SELECT {fn UCASE(Name)} FROM Employee  
```  
  
 下表列出使用函數逸出序列時，JDBC 驅動程式支援的各種函數：  
  
|字串函數|數值函數|日期時間函數|系統函數|  
|----------------------|-----------------------|------------------------|----------------------|  
|ASCII<br /><br /> CHAR<br /><br /> CONCAT<br /><br /> DIFFERENCE<br /><br /> INSERT<br /><br /> LCASE<br /><br /> LEFT<br /><br /> LENGTH<br /><br /> LOCATE<br /><br /> LTRIM<br /><br /> REPEAT<br /><br /> REPLACE<br /><br /> RIGHT<br /><br /> RTRIM<br /><br /> SOUNDEX<br /><br /> SPACE<br /><br /> SUBSTRING<br /><br /> UCASE|ABS<br /><br /> ACOS<br /><br /> ASIN<br /><br /> ATAN<br /><br /> ATAN2<br /><br /> CEILING<br /><br /> COS<br /><br /> COT<br /><br /> DEGREES<br /><br /> EXP<br /><br /> FLOOR<br /><br /> LOG<br /><br /> LOG10<br /><br /> MOD<br /><br /> PI<br /><br /> POWER<br /><br /> RADIANS<br /><br /> RAND<br /><br /> ROUND<br /><br /> SIGN<br /><br /> SIN<br /><br /> SQRT<br /><br /> TAN<br /><br /> TRUNCATE|CURDATE<br /><br /> CURTIME<br /><br /> DAYNAME<br /><br /> DAYOFMONTH<br /><br /> DAYOFWEEK<br /><br /> DAYOFYEAR<br /><br /> EXTRACT<br /><br /> HOUR<br /><br /> MINUTE<br /><br /> MONTH<br /><br /> MONTHNAME<br /><br /> NOW<br /><br /> QUARTER<br /><br /> SECOND<br /><br /> TIMESTAMPADD<br /><br /> TIMESTAMPDIFF<br /><br /> WEEK<br /><br /> YEAR|DATABASE<br /><br /> IFNULL<br /><br /> USER|  
  
> [!NOTE]  
>  如果您嘗試使用資料庫不支援的函數，將會發生錯誤。  
  
## <a name="date-and-time-literals"></a>日期和時間常值  
 日期、時間和時間戳記常值的逸出語法如下：  
  
```  
{literal-type 'value'}  
```  
  
 其中`literal-type`是下列其中之一：  
  
|常值類型|Description|值格式|  
|------------------|-----------------|------------------|  
|d|日期|yyyy-mm-dd|  
|t|Time|hh:mm:ss [1]|  
|ts|TimeStamp|yyyy-mm-dd hh:mm:ss[.f...]|  
  
 例如：  
  
```  
UPDATE Orders SET OpenDate={d '2005-01-31'}   
WHERE OrderID=1025  
```  
  
## <a name="stored-procedure-calls"></a>預存程序呼叫  
 JDBC 驅動程式支援`{? = call proc_name(?,...)}`和`{call proc_name(?,...)}`逸出語法的預存程序呼叫，視您是否需要處理傳回參數而定。  
  
 程序是一種儲存在資料庫中的可執行物件。 通常，它是先行編譯的一或多個 SQL 陳述式。 呼叫預存程序的逸出序列語法如下：  
  
```  
{[?=]call procedure-name[([parameter][,[parameter]]...)]}  
```  
  
 其中`procedure-name`指定預存程序的名稱和`parameter`指定預存程序參數。  
  
 如需有關使用`call`逸出序列與預存程序，請參閱[使用陳述式與預存程序](../../connect/jdbc/using-statements-with-stored-procedures.md)。  
  
## <a name="outer-joins"></a>外部聯結  
 JDBC 驅動程式支援 SQL92 左方外部聯結、右方外部聯結和完整外部聯結語法。 外部聯結的逸出序列如下：  
  
```  
{oj outer-join}  
```  
  
 其中 outer-join 為：  
  
```  
table-reference {LEFT | RIGHT | FULL} OUTER JOIN    
{table-reference | outer-join} ON search-condition  
```  
  
 其中`table-reference`資料表名稱和`search-condition`為您想要使用資料表的聯結條件。  
  
 例如：  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status   
   FROM {oj Customers LEFT OUTER JOIN   
      Orders ON Customers.CustID=Orders.CustID}   
   WHERE Orders.Status='OPEN'  
```  
  
 JDBC 驅動程式支援下列外部聯結逸出序列：  
  
-   左方外部聯結  
  
-   右方外部聯結  
  
-   完整外部聯結  
  
-   巢狀外部聯結  
  
## <a name="limit-escape-syntax"></a>LIMIT 逸出語法  
  
> [!NOTE]  
>  LIMIT 逸出語法只支援 Microsoft JDBC Driver 4.2 （或更高） for SQL Server 時使用 JDBC 4.1 或更高版本。  
  
 LIMIT 的逸出語法如下：  
  
```  
LIMIT <rows> [OFFSET <row offset>]  
```  
  
 逸出語法有兩個部分： \<*列*> 是必要項，指定要傳回的資料列數目。 位移和\<*資料列位移*> 為選擇性，指定開始傳回資料列之前要略過的資料列數目。 JDBC 驅動程式只支援必要的部分，方法是轉換查詢為使用 TOP，而非 LIMIT。 SQL Server 不支援 LIMIT 子句。 **JDBC 驅動程式不支援選擇性\<資料列位移 > 和驅動程式將會擲回例外狀況，則該值為使用**。  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與 JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
