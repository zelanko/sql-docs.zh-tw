---
title: 對應資料型態 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [ODBC]
- result sets [ODBC], data types
- ODBC data types, mapping
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], mapping
- sql_variant data type
- SQL Server Native Client ODBC driver, data types
ms.assetid: 4ba0924d-9fca-4c48-aced-0a8d817b3dde
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 92426c854758d07a9d62ec57510d202b870dd9f2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304620"
---
# <a name="mapping-data-types-odbc"></a>對應資料類型 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驅動程式 將 SQL 資料類型映射到 ODBC SQL 資料類型。 下列章節討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 資料類型和它們所對應的 ODBC SQL 資料類型。 這些章節也討論 ODBC SQL 資料類型及其對應的 ODBC C 資料類型，以及支援的和預設的轉換。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**時間戳**資料類型映射到SQL_BINARY或SQL_VARBINARY ODBC 數據類型,因為**時間戳**列中的值不是**日期時間**值,而是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指示行上活動序列的**二進位(8)** 或**varbinary(8)** 值。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式遇到奇數位元組的 SQL_C_WCHAR (Unicode) 值，則尾端的奇數位元組會被截斷。  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>處理 ODBC 中的 sql_variant 資料類型  
 **sql_variant**資料型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]態列 可以包含除大型物件 (LOB) 以外的任何資料類型,如**文字****、ntext**和**影像**。 例如,該列可以包含某些行**的較小值**、其他行的**浮動**值和其餘行中的**char/nchar**值。  
  
 **sql_variant**數據類型類似於 Microsoft 視覺化基本®中的**變體**資料類型。  
  
### <a name="retrieving-data-from-the-server"></a>從伺服器擷取資料  
 ODBC 沒有變體型態的概念,限制在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用**sql_variant**資料類型與 ODBC 驅動程式在 。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中,如果指定綁定,則**sql_variant**數據類型必須綁定到一個已記錄的 ODBC 數據類型。 **SQL_CA_SS_VARIANT_TYPE**(一個特定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]於 本機用戶端 ODBC 驅動程式的新屬性)將**sql_variant**列中實例的數據類型返回給使用者。  
  
 如果未指定繫結,[則 SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)函數可用於確定**sql_variant**列中實體的資料類型。  
  
 要檢索**sql_variant,** 請按照以下步驟操作。  
  
1.  調用**SQLFetch**以定位到檢索的行。  
  
2.  呼叫**SQLGetData**,為類型指定SQL_C_BINARY,為資料長度指定 0。 這將強制驅動程式讀取**sql_variant**標頭。 標頭在**sql_variant**列中提供該實例的數據類型。 **SQLGetData**傳回值的大小(以位元組為單位)。  
  
3.  通過將**SQL_CA_SS_VARIANT_TYPE**指定為其屬性值來呼叫[SQLColAttribute。](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 此函數將**sql_variant**列中實例的C數據類型返回給用戶端。  
  
 下列程式碼片段顯示前述的步驟。  
  
```  
while ((retcode = SQLFetch (hstmt))==SQL_SUCCESS)  
{  
    if (retcode != SQL_SUCCESS && retcode != SQL_SUCCESS_WITH_INFO)  
    {  
        SQLError (NULL, NULL, hstmt, NULL,   
                    &lNativeError,szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    retcode = SQLGetData (hstmt, 1, SQL_C_BINARY,   
                                pBuff,0,&Indicator);//Figure out the length  
    if (retcode != SQL_SUCCESS_WITH_INFO && retcode != SQL_SUCCESS)  
    {  
        SQLError (NULL, NULL, hstmt, NULL, &lNativeError,   
                    szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    printf_s ("Byte length : %d ",Indicator); //Print out the byte length  
  
    int iValue = 0;  
    retcode = SQLColAttribute (hstmt, 1, SQL_CA_SS_VARIANT_TYPE, NULL,   
                                        NULL,NULL,&iValue);  //Figure out the type  
    printf_s ("Sub type = %d ",iValue);//Print the type, the return is C_type of the column]  
  
// Set up a new binding or do the SQLGetData on that column with   
// the appropriate type  
}  
```  
  
 如果使用者使用[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)創建綁定,則驅動程式讀取元數據和數據。 驅動程式會接著將資料轉換為繫結中指定的適當 ODBC 類型。  
  
### <a name="sending-data-to-the-server"></a>將資料傳送到伺服器  
 **SQL_SS_VARIANT**(一種特定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]於 本機用戶端 ODBC 驅動程式的新數據類型)用於發送到**sql_variant**列的數據。 使用參數(例如,插入表名稱值(?,?))將資料發送到伺服器時[,SQLBind 參數](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)用於指定參數資訊,包括[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]C 類型和相應的類型。 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式將 C 數據類型轉換為適當的**sql_variant**子類型之一。  
  
## <a name="see-also"></a>另請參閱  
 [處理結果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
