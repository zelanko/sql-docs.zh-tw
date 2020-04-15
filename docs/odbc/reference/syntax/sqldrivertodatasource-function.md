---
title: SQLDrivertoDatasource 函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverToDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverToDataSource
helpviewer_keywords:
- SQLDriverToDataSource function [ODBC]
ms.assetid: 0de28eb5-8aa9-43e4-a87f-7dbcafe800dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7db7e4b20a35e047dca94cb72d8a6888fb670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302749"
---
# <a name="sqldrivertodatasource-function"></a>SQLDriverToDataSource 函式
**SQLDriverToDataSource**支援 ODBC 驅動程式的翻譯。 啟用 ODBC 的應用程式不調用此功能;應用程式透過**SQLSetConnect Attr**請求轉換。 與**SQLSetConnect Attr**中指定的*ConnectHandle*關聯的驅動程式呼叫指定的 DLL 以執行從驅動程式流向資料來源的所有資料的轉換。 可以在 ODBC 初始化檔中指定預設轉換 DLL。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLDriverToDataSource(  
     UDWORD     fOption,  
     SWORD      fSqlType,  
     PTR        rgbValueIn,  
     SDWORD     cbValueIn,  
     PTR        rgbValueOut,  
     SDWORD     cbValueOutMax,  
     SDWORD *   pcbValueOut,  
     UCHAR *    szErrorMsg,  
     SWORD      cbErrorMsgMax,  
     SWORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>引數  
 *fOption*  
 [輸入]選項值。  
  
 *fSqlType*  
 [輸入]ODBC SQL 資料類型。 此參數告訴驅動程式如何將*rgbValueIn*轉換為數據源可接受的窗體。 有關有效 SQL 資料類型的清單,請參考[SQL 資料型態](../../../odbc/reference/appendixes/sql-data-types.md)。  
  
 *rgbValuein*  
 [輸入]要翻譯的值。  
  
 *cbValuein*  
 [輸入]*rgbValue 的長度。*  
  
 *rgbValueOut*  
 【輸出]翻譯結果。  
  
> [!NOTE]  
>  轉換 DLL 不為 null 中止此值。  
  
 *cbValueOutMax*  
 [輸入]*rgbValueOut 的長度*。  
  
 *pcbValueOut*  
 【輸出]可在*rgbValueOut*中返回的位元組總數(不包括null終止位元組)。  
  
 對於字元或二進位數據,如果大於或等於*cbValueOutMax,**則 rgbValueOut*中的數據將被截斷為*cbValueOutMax*位元組。  
  
 對於所有其他數據類型,將忽略*cbValueOutMax*的值,轉換 DLL 假定*rgbValueOut*的大小是使用*fSqlType*指定的 SQL 資料類型的預設 C 數據類型的大小。  
  
 *pcbValueOut*參數可以是空指標。  
  
 *什洛姆斯格*  
 【輸出]指向存儲的錯誤消息。 這是一個空字串,除非翻譯失敗。  
  
 *cbErrorMsgMax*  
 [輸入]*szErrorMsg*的長度。  
  
 *多加錯姆斯格*  
 【輸出]指向可用在*szErrorMsg*返回的位元組總數(不包括空終止位元組)的指標。 如果大於或等於*cbErrorMsg,* 則*szErrorMsg*中的數據被截斷為*cbErrorMsgMax*減去 null 終止字元。 *pcbErrorMsg*參數可以是空指標。  
  
## <a name="returns"></a>傳回值  
 如果翻譯成功,則為 TRUE,如果翻譯失敗,則為 FALSE。  
  
## <a name="comments"></a>註解  
 驅動程式呼叫**SQLDriverToDataSource**將從驅動程式傳遞到資料來源的所有資料(SQL 語句、參數等)翻譯。 翻譯 DLL 可能不會翻譯某些資料,具體取決於資料的類型和翻譯 DLL 的用途。 例如,將字元數據從一個代碼頁轉換為另一個代碼頁的 DLL 忽略所有數位和二進位資料。  
  
 *fOption*的值設定為*vParam*的值,透過使用SQL_ATTR_TRANSLATE_OPTION屬性調用**SQLSetConnectAttr**指定。 它是一個 32 位值,對於給定的翻譯 DLL 具有特定的含義。 例如,它可以指定特定的字元集轉換。  
  
 如果為*rgbValueIn*和*rgbValueOut*指定了相同的緩衝區,則將就地執行緩衝區中數據的轉換。  
  
 雖然*cbValueIn、cbValueOutMax*和*pcbValueOut*是 SDWORD 的類型,但**SQLDriverToDataSource***cbValueIn*不一定支援巨大的指標。  
  
 如果**SQLDriverToDataSource**傳回 FALSE,則可能在轉換過程中發生數據截斷。 如果*pcbValueOut(* 輸出緩衝區中可返回的位元組數)大於*cbValueOutMax(* 輸出緩衝區的長度),則發生截斷。 驅動程序必須確定截斷是否可以接受。 如果未發生截斷 **,SQLDriverToDataSource**將由於另一個錯誤返回 FALSE。 在這兩種情況下,在*szErrorMsg*中返回特定的錯誤消息。  
  
 有關翻譯資料的詳細資訊,請參考[DLL](../../../odbc/reference/develop-app/translation-dlls.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|翻譯從資料來源傳回資料|[SQLDataSourceto 驅動程式](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|傳回連線屬性的設定|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連線屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
