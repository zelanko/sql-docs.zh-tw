---
title: "SQLDriverToDataSource 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0582038f1b1b89da041fde96e77bbdc47cad12a0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqldrivertodatasource-function"></a>SQLDriverToDataSource 函式
**SQLDriverToDataSource** ODBC 驅動程式支援翻譯。 啟用 ODBC 的應用程式; 不會呼叫此函式應用程式會要求透過轉譯**SQLSetConnectAttr**。 與相關聯的驅動程式*ConnectionHandle*中所指定**SQLSetConnectAttr**呼叫指定的 DLL，以執行資料驅動程式傳輸至資料來源的翻譯。 ODBC 初始設定檔案中，可以指定的預設轉譯 DLL。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 [輸入]ODBC SQL 資料型別。 這個引數會指示驅動程式如何將轉換*rgbValueIn*成資料來源可接受格式。 如需有效的 SQL 資料類型的清單，請參閱[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)。  
  
 *rgbValueIn*  
 [輸入]要轉譯的值。  
  
 *cbValueIn*  
 [輸入]長度*rgbValueIn*。  
  
 *rgbValueOut*  
 [輸出]轉換的結果。  
  
> [!NOTE]  
>  轉譯 DLL 不會不 null 結尾的這個值。  
  
 *cbValueOutMax*  
 [輸入]長度*rgbValueOut*。  
  
 *pcbValueOut*  
 [輸出]的總位元組數 （不含 null 結束位元組） 可用來傳回中*rgbValueOut*。  
  
 字元或二進位資料時，如果這是大於或等於*cbValueOutMax*中的資料*rgbValueOut*會被截斷成*cbValueOutMax*位元組。  
  
 對於所有其他資料類型，值*cbValueOutMax*會忽略並轉譯 DLL 假設大小*rgbValueOut*是與指定的SQL資料類型的預設C資料類型的大小*fSqlType*。  
  
 *PcbValueOut*引數可以是 null 指標。  
  
 *szErrorMsg*  
 [輸出]儲存體的錯誤訊息的指標。 除非轉譯失敗，這會是空字串。  
  
 *cbErrorMsgMax*  
 [輸入]長度*szErrorMsg*。  
  
 *pcbErrorMsg*  
 [輸出]指標的總位元組數 （不含 null 結束位元組） 可用來傳回中*szErrorMsg*。 如果這是大於或等於*cbErrorMsg*中的資料*szErrorMsg*會被截斷成*cbErrorMsgMax*減去 null 結束字元。 *PcbErrorMsg*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果轉換成功，FALSE 轉譯失敗時，則為 TRUE。  
  
## <a name="comments"></a>註解  
 驅動程式呼叫**SQLDriverToDataSource**轉譯 （SQL 陳述式、 參數等等） 的所有資料將從驅動程式傳遞至資料來源。 轉譯 DLL 可能不會轉譯部分資料，取決於資料的型別和轉譯 DLL 的用途。 例如，轉譯字元資料從一個字碼頁之間的 DLL 會忽略所有的數字和二進位資料。  
  
 值*fOption*設定的值為*vParam*指定藉由呼叫**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 屬性。 它是 32 位元值，指定翻譯 DLL 特定的意義。 例如，它可以指定特定字元集轉譯。  
  
 如果指定在相同緩衝區*rgbValueIn*和*rgbValueOut*，翻譯的緩衝區中的資料將會執行備妥。  
  
 雖然*cbValueIn*， *cbValueOutMax*，和*pcbValueOut*類型 SDWORD， **SQLDriverToDataSource**並不一定會支援大型的指標。  
  
 如果**SQLDriverToDataSource**會傳回 FALSE，轉譯期間可能發生資料截斷。 如果*pcbValueOut* （可用來傳回在輸出緩衝區的位元組數） 會大於*cbValueOutMax* （輸出緩衝區的長度），則發生截斷。 驅動程式必須判斷已可接受的截斷。 如果未發生截斷， **SQLDriverToDataSource**因其他錯誤而傳回 FALSE。 在任一情況下，傳回特定的錯誤訊息中*szErrorMsg*。  
  
 如需轉譯資料的詳細資訊，請參閱[轉譯 Dll](../../../odbc/reference/develop-app/translation-dlls.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|轉譯資料所傳回的資料來源|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
