---
title: SQLDriverToDataSource 函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d36996f49cb58fbb8812ae5fee8928fdc8bddf1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104643"
---
# <a name="sqldrivertodatasource-function"></a>SQLDriverToDataSource 函式
**SQLDriverToDataSource**支援 ODBC 驅動程式的翻譯。 此函式不是由具備 ODBC 功能的應用程式所呼叫;應用程式會透過**SQLSetConnectAttr**要求轉譯。 與**SQLSetConnectAttr**中指定的*ConnectionHandle*相關聯的驅動程式會呼叫指定的 DLL，以執行從驅動程式流向資料來源之所有資料的翻譯。 預設的轉譯 DLL 可以在 ODBC 初始化檔中指定。  
  
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
 源選項值。  
  
 *fSqlType*  
 源ODBC SQL 資料類型。 這個引數會告訴驅動程式如何將*rgbValueIn*轉換成資料來源可接受的表單。 如需有效 SQL 資料類型的清單，請參閱[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)。  
  
 *rgbValueIn*  
 源要轉譯的值。  
  
 *cbValueIn*  
 源*RgbValueIn*的長度。  
  
 *rgbValueOut*  
 輸出轉譯的結果。  
  
> [!NOTE]  
>  轉譯 DLL 不會以 null 終止此值。  
  
 *cbValueOutMax*  
 源*RgbValueOut*的長度。  
  
 *pcbValueOut*  
 輸出可在*rgbValueOut*中傳回的總位元組數（不包括 null 終止位元組）。  
  
 對於字元或二進位資料，如果這個大於或等於*cbValueOutMax*， *rgbValueOut*中的資料會被截斷為*cbValueOutMax*位元組。  
  
 對於所有其他資料類型，會忽略*cbValueOutMax*的值，且轉譯 DLL 會假設*rgbValueOut*的大小是使用*fSqlType*所指定之 SQL 資料類型的預設 C 資料類型大小。  
  
 *PcbValueOut*引數可以是 null 指標。  
  
 *szErrorMsg*  
 輸出錯誤訊息的儲存體指標。 除非轉譯失敗，否則這是空字串。  
  
 *cbErrorMsgMax*  
 源*SzErrorMsg*的長度。  
  
 *pcbErrorMsg*  
 輸出可在*szErrorMsg*中傳回的位元組總數（不包括 null 終止位元組）的指標。 如果此值大於或等於*cbErrorMsg*， *szErrorMsg*中的資料會被截斷為*cbErrorMsgMax*減去 null 終止字元。 *PcbErrorMsg*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果轉譯成功，則為 TRUE，如果轉譯失敗則為 FALSE。  
  
## <a name="comments"></a>註解  
 驅動程式會呼叫**SQLDriverToDataSource**來轉譯從驅動程式傳遞至資料來源的所有資料（SQL 語句、參數等等）。 轉譯 DLL 可能無法轉譯某些資料，視資料的類型和轉譯 DLL 的目的而定。 例如，將某個字碼頁的字元資料轉譯為另一個的 DLL，會忽略所有數值和二進位資料。  
  
 *FOption*的值會設定為使用 SQL_ATTR_TRANSLATE_OPTION 屬性呼叫**SQLSetConnectAttr**所指定的*vParam*值。 它是32位的值，對於給定的轉譯 DLL 具有特定意義。 例如，它可以指定特定的字元集轉譯。  
  
 如果為*rgbValueIn*和*rgbValueOut*指定相同的緩衝區，則會就地執行緩衝區中的資料轉譯。  
  
 雖然*cbValueIn*、 *cbValueOutMax*和*pcbValueOut*的類型為 SDWORD，但**SQLDriverToDataSource**不一定支援大指標。  
  
 如果**SQLDriverToDataSource**傳回 FALSE，則表示轉譯期間可能發生資料截斷。 如果*pcbValueOut* （可在輸出緩衝區中傳回的位元組數目）大於*cbValueOutMax* （輸出緩衝區的長度），則會發生截斷。 驅動程式必須判斷是否可接受截斷。 如果未發生截斷， **SQLDriverToDataSource**會因為另一個錯誤而傳回 FALSE。 不論是哪一種情況， *szErrorMsg*中都會傳回特定的錯誤訊息。  
  
 如需翻譯資料的詳細資訊，請參閱[轉譯 dll](../../../odbc/reference/develop-app/translation-dlls.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|翻譯從資料來源傳回的資料|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
