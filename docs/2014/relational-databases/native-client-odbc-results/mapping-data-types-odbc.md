---
title: 對應資料類型 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd657592598ad51a2a61d0f51e5e36cbf56067c5
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423557"
---
# <a name="mapping-data-types-odbc"></a>對應資料類型 (ODBC)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至 ODBC SQL 資料類型的 SQL 資料類型。 下列章節討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 資料類型和它們所對應的 ODBC SQL 資料類型。 這些章節也討論 ODBC SQL 資料類型及其對應的 ODBC C 資料類型，以及支援的和預設的轉換。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**時間戳記**資料類型與 SQL_BINARY 或 SQL_VARBINARY ODBC 資料類型，因為中的值**時間戳記**資料行不是**datetime**值，但**binary(8**或**varbinary(8**值，指出序列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料列上的活動。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式遇到奇數位元組的 SQL_C_WCHAR (Unicode) 值，則尾端的奇數位元組會被截斷。  
  
## <a name="dealing-with-sqlvariant-data-type-in-odbc"></a>處理 ODBC 中的 sql_variant 資料類型  
 **Sql_variant**資料類型資料行可以包含任何資料類型，在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除大型物件 (Lob)**文字**， **ntext**，以及**映像**。 比方說，資料行可以包含**smallint**某些資料列的值**float**值的其他資料列，並**char/nchar**其餘部分的值。  
  
 **Sql_variant**資料類型是類似**Variant** Microsoft Visual Basic® 中的資料類型。  
  
### <a name="retrieving-data-from-the-server"></a>從伺服器擷取資料  
 ODBC 沒有變數的類型，概念限制使用**sql_variant** ODBC 驅動程式中使用的資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，如果指定繫結，則**sql_variant**資料型別必須繫結至其中一個所記錄的 ODBC 資料類型。 **SQL_CA_SS_VARIANT_TYPE**，以特定的新屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，傳回的資料類型之執行個體**sql_variant**給使用者的資料行。  
  
 如果未不指定任何繫結，則[SQLGetData](../native-client-odbc-api/sqlgetdata.md)函式可以用來判斷執行個體中的資料型別**sql_variant**資料行。  
  
 若要擷取**sql_variant**資料，請遵循下列步驟。  
  
1.  呼叫**SQLFetch**來定位到擷取的資料列。  
  
2.  呼叫**SQLGetData**，指定 SQL_C_BINARY 的型別和資料長度為 0。 這會強制驅動程式會讀取**sql_variant**標頭。 標頭提供該執行個體中的資料型別**sql_variant**資料行。 **SQLGetData**傳回之值的大小 （以位元組為單位）。  
  
3.  呼叫[SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md)藉由指定**SQL_CA_SS_VARIANT_TYPE**做為其屬性值。 此函式會傳回 C 資料類型之執行個體**sql_variant**給用戶端的資料行。  
  
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
  
 如果使用者建立繫結使用[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)，驅動程式會讀取中繼資料和資料。 驅動程式會接著將資料轉換為繫結中指定的適當 ODBC 類型。  
  
### <a name="sending-data-to-the-server"></a>將資料傳送到伺服器  
 **SQL_SS_VARIANT**的新資料型別特有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，用於資料傳送至**sql_variant**資料行。 將資料傳送至使用參數的伺服器時 (例如，INSERT INTO TableName VALUES (？，？))， [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)用來指定的參數資訊，包括 C 類型和對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]型別。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會將 C 資料類型轉換成其中一個適當**sql_variant**子類型。  
  
## <a name="see-also"></a>另請參閱  
 [處理結果&#40;ODBC&#41;](processing-results-odbc.md)  
  
  
