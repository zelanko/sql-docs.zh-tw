---
title: 使用 SQL_NUMERIC_STRUCT 取出數值資料 |Microsoft Docs
description: 使用 ODBC 的 c/c + + 會使用與 SQL_C_NUMERIC 相關的 SQL_NUMERIC_STRUCT 來抓取 SQL Server 數值資料類型。
editor: ''
ms.prod: sql
ms.technology: ''
ms.devlang: cpp
ms.topic: conceptual
ms.custom: ''
ms.date: 07/13/2017
ms.author: genemi
author: MightyPen
ms.openlocfilehash: 296a6bd9b5e0ab64fe7ecc7d78924a02e5fda9cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057194"
---
# <a name="retrieve-numeric-data-with-sql_numeric_struct"></a>使用 SQL\_數值\_結構取出數值資料

本文描述如何從 SQL Server ODBC 驅動程式中，將數值資料取出成數值結構。 它也會說明如何使用特定的精確度和小數位數值來取得正確的值。

此資料類型可讓應用程式直接處理數值資料。 在2003年，odbc 3.0 引進了**\_SQL c\_數值**所識別的新 odbc C 資料類型。 此資料類型仍然與2017相關。

使用的 C 緩衝區具有**\_SQL 數值\_結構**的類型定義。 這個結構的欄位可用於儲存數值資料的有效位數、小數位數、正負號和數值。 值本身會儲存為相應的整數，且最小的位元組是從最左邊的位置開始。 

[C 資料類型](c-data-types.md)一文提供有關 SQL\_數值\_結構的格式和使用的詳細資訊。 ODBC 3.0 程式設計人員參考的[附錄 D](appendix-d-data-types.md)通常會討論資料類型。


## <a name="sql_numeric_struct-overview"></a>SQL\_數值\_結構總覽


SQL\_數值\_結構定義于 sqltypes 標頭檔中，如下所示：


```c
#define SQL_MAX_NUMERIC_LEN    16
typedef struct tagSQL_NUMERIC_STRUCT
{
   SQLCHAR    precision;
   SQLSCHAR   scale;
   SQLCHAR    sign;   /* 1 if positive, 0 if negative */
   SQLCHAR    val[SQL_MAX_NUMERIC_LEN];
} SQL_NUMERIC_STRUCT;
```

            
數值結構的有效位數和小數位數位段永遠不會用於應用程式的輸入，只用于從驅動程式輸出到應用程式。

此驅動程式會在每次將資料傳回給應用程式時，使用預設精確度（驅動程式定義）和預設小數位數（0）。 除非應用程式指定有效位數和小數位數的值，否則驅動程式會假設預設值，並截斷數值資料的小數部分。

## <a name="sql_numeric_struct-code-sample"></a>SQL\_數值\_結構程式碼範例

此程式碼範例示範如何：

- 設定精確度。
- 設定尺規。
- 取得正確的值。 

> [!Note]
> 您在本文中所提供的程式碼所使用的任何功能，都是您自己的風險。 
>
> Microsoft 提供這些程式碼範例，但不含任何明示或默示的擔保，包括但不限於適售性和（或）適合特定用途的默示擔保。

```c
#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <stdlib.h>
#include <ctype.h>
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

#define MAXDSN       25
#define MAXUID       25
#define MAXAUTHSTR   25
#define MAXBUFLEN   255

SQLHENV     henv   = SQL_NULL_HENV;
SQLHDBC     hdbc1  = SQL_NULL_HDBC;     
SQLHSTMT    hstmt1 = SQL_NULL_HSTMT;
SQLHDESC    hdesc  = NULL;


SQL_NUMERIC_STRUCT NumStr;

int main()
{
   RETCODE retcode;

//Change the values below as appropriate to make a successful connection.
//szDSN: DataSourceName, szUID=userid, szAuthStr: password

UCHAR szDSN[MAXDSN+1] = "sql33",szUID[MAXUID+1]="sa", szAuthStr[MAXAUTHSTR+1] = "";
SQLINTEGER strlen1;
SQLINTEGER a;
int i,sign =1;
long myvalue, divisor;
float final_val;
   
// Allocate the Environment handle. Set the Env attribute, allocate the
//connection handle, connect to the database and allocate the statement //handle.

retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);
retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION,(SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);
retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);
retcode = SQLConnect(hdbc1, szDSN,SQL_NTS,szUID,SQL_NTS,szAuthStr,SQL_NTS);
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);

// Execute the select statement. Here it is assumed that numeric_test
//table is created using the following statements:

// Create table numeric_test (col1 numeric(5,3))
//insert into numeric_test values (25.212)

retcode = SQLExecDirect(hstmt1,(UCHAR *)"select * from numeric_test",SQL_NTS);

// Use SQLBindCol to bind the NumStr to the column that is being retrieved.

retcode = SQLBindCol(hstmt1,1,SQL_C_NUMERIC,&NumStr,19,&strlen1);

// Get the application row descriptor for the statement handle using
//SQLGetStmtAttr.

retcode = SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_ROW_DESC,&hdesc, 0, NULL);

// You can either use SQLSetDescRec or SQLSetDescField when using
// SQLBindCol. However, if you prefer to call SQLGetData, you have to
// call SQLSetDescField instead of SQLSetDescRec. For more information on
// descriptors, please refer to the ODBC 3.0 Programmers reference or
// your Online documentation.

//Used when using SQLSetDescRec
//a=b=sizeof(NumStr);

// Set the datatype, precision and scale fields of the descriptor for the 
//numeric column. Otherwise the default precision (driver defined) and 
//scale (0) are returned.

// In this case, the table contains only one column, hence the second 
//parameter contains one. Zero applies to bookmark columns. Please check 
//the programmers guide for more information.

//retcode=SQLSetDescRec(hdesc,1,SQL_NUMERIC,NULL,sizeof(NumStr),5,3,&NumStr,&a,&b);

retcode = SQLSetDescField (hdesc,1,SQL_DESC_TYPE,(VOID*)SQL_C_NUMERIC,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_PRECISION,(VOID*) 5,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_SCALE,(VOID*) 3,0);
    
// Initialize the val array in the numeric structure.

memset(NumStr.val,0,16);
   
// Call SQLFetch to fetch the first record.

while((retcode =SQLFetch(hstmt1)) != SQL_NO_DATA)
  {
// Notice that the TargetType (3rd Parameter) is SQL_ARD_TYPE, which  
//forces the driver to use the Application Row Descriptor with the 
//specified scale and precision.

   retcode = SQLGetData(hstmt1, 1, SQL_ARD_TYPE, &NumStr, 19, &a); 

// Check for null indicator.

   if ( SQL_NULL_DATA == a )
   {
   printf( "The final value: NULL\n" );
   continue;
   }

// Call to convert the little endian mode data into numeric data.

   myvalue = strtohextoval();

// The returned value in the above code is scaled to the value specified
//in the scale field of the numeric structure. For example 25.212 would
//be returned as 25212. The scale in this case is 3 hence the integer 
//value needs to be divided by 1000.

   divisor = 1;
   if(NumStr.scale > 0)
     {
    for (i=0;i< NumStr.scale; i++)   
         divisor = divisor * 10;
     }
   final_val =  (float) myvalue /(float) divisor;

// Examine the sign value returned in the sign field for the numeric
//structure.
//NOTE: The ODBC 3.0 spec required drivers to return the sign as 
//1 for positive numbers and 2 for negative number. This was changed in the
//ODBC 3.5 spec to return 0 for negative instead of 2.

      if(!NumStr.sign) sign = -1;
      else sign  =1;

   final_val *= sign;
   printf("The final value: %f\n",final_val);
    }

   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA_FOUND);

   /* clean up */ 
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);
   SQLDisconnect(hdbc1);
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
   return(0);
}
```


### <a name="interim-results"></a>過渡結果：


```console
//  C  ==> 12 * 1    =     12
//  7  ==> 07 * 16   =    112
//  2  ==> 02 * 256  =    512
//  6  ==> 06 * 4096 =  24576
===============================
                 Sum =  25212
```


在數值結構中，val 欄位是16個元素的字元陣列。 例如，25.212 會調整為25212，而小數值則為3。 在十六進位格式中，這個數位會是627C。

驅動程式會傳回下列專案：

- 7C 的對等字元，也就是 ' | '字元陣列的第一個元素中的（管道）。
- 等同于62，也就是第二個元素中的 ' b '。
- 陣列元素的餘數包含零，因此緩衝區包含 ' | b\0 '。

現在的挑戰是要從這個字串陣列中，建立相應縮小的整數。 字串中的每個字元都對應到兩個十六進位數位，也就是最低有效位數（LSD）和最重要的數位（MSD）。 從1開始，可以將每個數位（LSD & MSD）與16的倍數相乘來產生縮放的整數值。

程式碼，可從極小的 endian 模式轉換成相應的整數。 應用程式開發人員可自行決定是否要執行這種功能。 下列程式碼範例只是其中一種可能的方法。


```c
long strtohextoval()
{
    long val=0,value=0;
    int i=1,last=1,current;
    int a=0,b=0;

        for(i=0;i<=15;i++)
        {
         current = (int) NumStr.val[i];
         a= current % 16; //Obtain LSD
         b= current / 16; //Obtain MSD
            
         value += last* a;   
         last = last * 16;   
         value += last* b;
         last = last * 16;   
        }
     return value;
}
```


### <a name="applies-to-versions"></a>適用于版本


關於 SQL\_數值\_結構的上述資訊適用于下列產品版本：

- Microsoft ODBC Driver for Microsoft SQL Server 3。7
- Microsoft Data Access Components 2。1
- Microsoft Data Access Components 2。5
- Microsoft Data Access Components 2。6
- Microsoft Data Access Components 2。7


## <a name="sql_c_numeric-overview"></a>SQL\_C\_數值總覽


下列範例程式說明如何使用 SQL\_C\_數值，方法是將123.45 插入資料表。 在資料表中，資料行會定義為數值或十進位，且有效位數為5，而資料行則是小數位數2。

您用來執行此程式的 ODBC 驅動程式必須支援 ODBC 3.0 功能。


```c
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

void main() {

   SQLHENV    henv  = NULL;
   SQLHDBC    hdbc  = NULL;
   SQLHSTMT   hstmt = NULL;

   SQL_NUMERIC_STRUCT   NumStr;
   SQLINTEGER           cbNumStr = sizeof (NumStr);

   SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);

   /* Set the ODBC behavior version. */ 
   SQLSetEnvAttr(henv,
         SQL_ATTR_ODBC_VERSION,
         (SQLPOINTER) SQL_OV_ODBC3,
         SQL_IS_INTEGER);

   SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);

   /* Substitute your own connection information */ 
   SQLConnect(hdbc,
      (SQLCHAR *) "MyDSN", 5,
      (SQLCHAR *) "UserID", 6,
      (SQLCHAR *) "Password", 8);

   SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);

   /*
      Set up the SQL_NUMERIC_STRUCT, NumStr, to hold "123.45".

      First, we need to scale 123.45 to an integer: 12345
      One way to switch the bytes is to convert 12345 to Hex:  0x3039
      Since the least significant byte will be stored starting from the
      leftmost byte, "0x3039" will be stored as "0x3930".

      The precision and scale fields are not used for input to the driver,
      only for output from the driver. The precision and scale will be set
      in the application parameter descriptor later.
   */ 

   NumStr.sign = 1;   /* 1 if positive, 2 if negative */ 

   memset (NumStr.val, 0, 16);
   NumStr.val [0] = 0x39;
   NumStr.val [1] = 0x30;

   /* SQLBindParameter needs to be called before SQLSetDescField */ 
   SQLBindParameter(hstmt,
          1,
          SQL_PARAM_INPUT,
          SQL_C_NUMERIC,
          SQL_NUMERIC,
          5,
          2,
          &NumStr,
          0,
          (SQLINTEGER *) &cbNumStr);

   /* Modify the fields in the implicit application parameter descriptor */ 
   SQLHDESC   hdesc = NULL;

   SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);
   SQLSetDescField(hdesc, 1, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_PRECISION, (SQLPOINTER) 5, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_SCALE, (SQLPOINTER) 2, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_DATA_PTR, (SQLPOINTER) &NumStr, 0);

   SQLExecDirect(hstmt,
         (SQLCHAR *) "INSERT INTO table (numeric_column) VALUES (?)",
         SQL_NTS);

   SQLFreeHandle(SQL_HANDLE_STMT, hstmt);

   SQLDisconnect (hdbc);

   SQLFreeHandle(SQL_HANDLE_DBC, hdbc);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
}
```


<!--
GeneMi historical notes, 2017/July/12. Per Jason.C

https://go.microsoft.com/fwlink/?LinkId=147596

https://support.microsoft.com/help/222831

https://web.archive.org/web/20140319133434/http:/support.microsoft.com:80/kb/222831

https://web.archive.org/web/20080505073901/http:/support.microsoft.com:80/kb/181254

https://docs.microsoft.com/sql/odbc/reference/appendixes/c-data-types
-->

