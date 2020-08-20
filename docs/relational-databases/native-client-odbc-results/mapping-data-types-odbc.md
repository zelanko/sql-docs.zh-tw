---
description: 對應資料類型 (ODBC)
title: " (ODBC) 對應資料類型 |Microsoft Docs"
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
ms.openlocfilehash: a2cd0786cac3976bcb280422f177d19d8f86a3c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465298"
---
# <a name="mapping-data-types-odbc"></a>對應資料類型 (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sql 資料類型對應至 ODBC sql 資料類型。 下列章節討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 資料類型和它們所對應的 ODBC SQL 資料類型。 這些章節也討論 ODBC SQL 資料類型及其對應的 ODBC C 資料類型，以及支援的和預設的轉換。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**時間戳記**資料類型會對應至 SQL_BINARY 或 SQL_VARBINARY ODBC 資料類型，因為**時間戳記**資料行中的值不是**日期時間**值，而是**二進位 (8) **或**VARBINARY (8) **表示資料列活動順序的值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式遇到奇數位元組的 SQL_C_WCHAR (Unicode) 值，則尾端的奇數位元組會被截斷。  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>處理 ODBC 中的 sql_variant 資料類型  
 **Sql_variant**資料類型資料行可包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (lob) 的大型物件（例如**text**、 **Ntext**和**image**）以外的任何資料類型。 例如，資料行可能包含某些資料列的 **Smallint** 值、其他資料列的 **float** 值，以及餘數中的 **char/Nchar** 值。  
  
 **Sql_variant**資料類型類似于 Microsoft Visual Basic®中的**variant**資料類型。  
  
### <a name="retrieving-data-from-the-server"></a>從伺服器擷取資料  
 ODBC 沒有 variant 型別的概念，限制在中使用 **SQL_variant** 資料類型與 ODBC 驅動程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，如果指定了 binding， **SQL_variant** 資料類型必須系結至其中一個記載的 ODBC 資料類型。 **SQL_CA_SS_VARIANT_TYPE**（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式特定的新屬性）會將 **SQL_variant** 資料行中實例的資料類型傳回給使用者。  
  
 如果未指定系結，則可以使用 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 函數來判斷 **SQL_variant** 資料行中實例的資料類型。  
  
 若要取出 **SQL_variant** 資料，請遵循下列步驟。  
  
1.  呼叫 **SQLFetch** ，以定位至抓取的資料列。  
  
2.  呼叫 **SQLGetData**，指定類型的 SQL_C_BINARY，並指定0作為資料長度。 這會強制驅動程式讀取 **SQL_variant** 標頭。 標頭會提供該實例在 **SQL_variant** 資料行中的資料類型。 **SQLGetData** 會傳回值的大小 (以位元組為單位) 。  
  
3.  藉由將**SQL_CA_SS_VARIANT_TYPE**指定為其屬性值來呼叫[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 。 此函數會將 **SQL_variant** 資料行中實例的 C 資料類型傳回給用戶端。  
  
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
  
 如果使用者使用 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)建立系結，驅動程式會讀取中繼資料和資料。 驅動程式會接著將資料轉換為繫結中指定的適當 ODBC 類型。  
  
### <a name="sending-data-to-the-server"></a>將資料傳送到伺服器  
 **SQL_SS_VARIANT**（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式特定的新資料類型）用於傳送至 **SQL_variant** 資料行的資料。 使用參數將資料傳送至伺服器時 (例如，插入 TableName 值 (?,? ) # A3， [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 可用來指定參數資訊，包括 C 型別和對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型別。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會將 C 資料類型轉換成其中一個適當的**SQL_variant**子類型。  
  
## <a name="see-also"></a>另請參閱  
 [處理 &#40;ODBC&#41;的結果 ](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
