---
title: "對應資料類型 (ODBC) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
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
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7e8b33636ef971744cfe006a4750416dc750e0fd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="mapping-data-types-odbc"></a>對應資料類型 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至 ODBC SQL 資料類型的 SQL 資料類型。 下列章節討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 資料類型和它們所對應的 ODBC SQL 資料類型。 這些章節也討論 ODBC SQL 資料類型及其對應的 ODBC C 資料類型，以及支援的和預設的轉換。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**時間戳記**資料類型與 SQL_BINARY 或 SQL_VARBINARY ODBC 資料類型，因為中的值**時間戳記**資料行不是**datetime**值，但**binary （8)**或**varbinary （8)**值，指出一連串[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料列上的活動。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式遇到奇數位元組的 SQL_C_WCHAR (Unicode) 值，則尾端的奇數位元組會被截斷。  
  
## <a name="dealing-with-sqlvariant-data-type-in-odbc"></a>處理 ODBC 中的 sql_variant 資料類型  
 **Sql_variant**資料類型資料行可以包含任何資料類型，在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除了大型物件 (Lob)，例如**文字**， **ntext**，和**映像**。 例如，資料行可能包含**smallint**某些資料列的值**float**其他資料列，值和**char/nchar**其餘部分中的值。  
  
 **Sql_variant**資料類型會類似於**Variant** Microsoft Visual Basic® 中的資料類型。  
  
### <a name="retrieving-data-from-the-server"></a>從伺服器擷取資料  
 ODBC 沒有變數的類型的概念限制使用**sql_variant**透過 ODBC 驅動程式中的資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則會指定繫結， **sql_variant**記載的 ODBC 資料類型的其中一個必須繫結資料型別。 **SQL_CA_SS_VARIANT_TYPE**，新屬性的特定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，傳回的資料類型之執行個體**sql_variant**給使用者的資料行。  
  
 如果未不指定任何繫結，則[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)函式可用來判斷執行個體中的資料型別**sql_variant**資料行。  
  
 若要擷取**sql_variant**資料，請遵循下列步驟。  
  
1.  呼叫**SQLFetch**來定位到擷取的資料列。  
  
2.  呼叫**SQLGetData**，指定 SQL_C_BINARY 類型和資料長度為 0。 這會強制驅動程式來讀取**sql_variant**標頭。 標頭提供該執行個體中的資料型別**sql_variant**資料行。 **SQLGetData**傳回之值的大小 （以位元組為單位）。  
  
3.  呼叫[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)藉由指定**SQL_CA_SS_VARIANT_TYPE**做為其屬性值。 此函式會傳回執行個體中的 C 資料類型**sql_variant**給用戶端的資料行。  
  
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
  
 如果使用者建立的繫結使用[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)，驅動程式會讀取中繼資料和資料。 驅動程式會接著將資料轉換為繫結中指定的適當 ODBC 類型。  
  
### <a name="sending-data-to-the-server"></a>將資料傳送到伺服器  
 **SQL_SS_VARIANT**、 新的資料類型的特定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，用於傳送至資料**sql_variant**資料行。 將資料傳送至使用參數的伺服器時 (例如，INSERT INTO TableName VALUES (？，？))， [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)用來指定包含 C 類型和對應的參數資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]型別。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會將 C 資料類型轉換成其中一個適當**sql_variant**子類型。  
  
## <a name="see-also"></a>請參閱＜  
 [處理結果 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
