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
manager: craigg
ms.openlocfilehash: 844e11e72bb46b69229a9a4747ac7e64f013f14e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537163"
---
# <a name="sqldrivertodatasource-function"></a>SQLDriverToDataSource 函式
**SQLDriverToDataSource** ODBC 驅動程式支援翻譯。 啟用 ODBC 的應用程式; 不會呼叫此函式應用程式會要求透過翻譯**SQLSetConnectAttr**。 驅動程式相關聯*ConnectionHandle*中指定**SQLSetConnectAttr**呼叫指定的 DLL，以執行從驅動程式傳輸到資料來源的所有資料的翻譯。 ODBC 初始化檔案中，就可以指定的預設轉譯 DLL。  
  
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
 [輸入]ODBC SQL 資料型別。 此引數會指示驅動程式如何將轉換*rgbValueIn*成資料來源可接受的格式。 如需有效的 SQL 資料類型的清單，請參閱 < [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)。  
  
 *rgbValueIn*  
 [輸入]要轉譯的值。  
  
 *cbValueIn*  
 [輸入]長度*rgbValueIn*。  
  
 *rgbValueOut*  
 [輸出]轉譯結果。  
  
> [!NOTE]  
>  轉譯 DLL 不會不 null 結尾的這個值。  
  
 *cbValueOutMax*  
 [輸入]長度*rgbValueOut*。  
  
 *pcbValueOut*  
 [輸出]的總位元組數 （不含終止 null 位元組） 可用以傳回*rgbValueOut*。  
  
 針對字元或二進位資料，如果這是大於或等於*cbValueOutMax*中的資料*rgbValueOut*會被截斷成*cbValueOutMax*位元組。  
  
 對於所有其他資料類型，值*cbValueOutMax*會忽略並轉譯 DLL 假設的大小*rgbValueOut* 與指定的SQL資料類型的預設C資料類型的大小*fSqlType*。  
  
 *PcbValueOut*引數可以是 null 指標。  
  
 *szErrorMsg*  
 [輸出]錯誤訊息的儲存體的指標。 除非無法轉譯，這會是空字串。  
  
 *cbErrorMsgMax*  
 [輸入]長度*szErrorMsg*。  
  
 *pcbErrorMsg*  
 [輸出]指標的總位元組數 （不含終止 null 位元組） 可用以傳回*szErrorMsg*。 如果這是大於或等於*cbErrorMsg*中的資料*szErrorMsg*會被截斷成*cbErrorMsgMax*減去之 null 結束字元。 *PcbErrorMsg*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果轉換成功，FALSE 如果轉換失敗，則為 TRUE。  
  
## <a name="comments"></a>註解  
 驅動程式呼叫**SQLDriverToDataSource**翻譯 （SQL 陳述式、 參數等等） 的所有資料將從驅動程式傳遞至資料來源。 轉譯 DLL 可能不會轉譯部分資料，視資料的型別和轉譯 DLL 的目的而定。 例如，轉譯至另一個字碼頁的字元資料的 DLL 會忽略所有的數字和二進位資料。  
  
 值*fOption*設定的值為*vParam*藉由呼叫指定**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 屬性。 它是具有特定意義的特定轉譯 DLL 的 32 位元值。 比方說，它可以指定特定的字元設定轉譯。  
  
 如果指定了相同的緩衝區*rgbValueIn*並*rgbValueOut*，翻譯的緩衝區中的資料將會執行就地。  
  
 雖然*cbValueIn*， *cbValueOutMax*，並*pcbValueOut* SDWORD，類型**SQLDriverToDataSource**不一定支援大型的指標。  
  
 如果**SQLDriverToDataSource**傳回 FALSE，可能會在轉譯期間發生資料截斷。 如果*pcbValueOut* （可用來傳回輸出緩衝區中的位元組數字） 大於*cbValueOutMax* （輸出緩衝區的長度），則發生截斷。 驅動程式必須判斷已可接受的截斷。 如果未發生截斷，一樣**SQLDriverToDataSource**因其他錯誤而傳回 FALSE。 在任一情況下，特定的錯誤訊息傳入*szErrorMsg*。  
  
 如需有關轉譯資料的詳細資訊，請參閱[轉譯 Dll](../../../odbc/reference/develop-app/translation-dlls.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|轉譯資料傳回資料來源|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
