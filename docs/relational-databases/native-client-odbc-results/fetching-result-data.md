---
title: 提取結果資料 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLFetchScroll function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], fetching
- SQLBindCol function
- result sets [ODBC], fetching
- fetching [ODBC]
- ODBC data types, fetching
- SQLFetch function
- SQL Server Native Client ODBC driver, data types
- SQLGetData function
ms.assetid: b289c7fb-5017-4d7e-a2d3-19401e9fc4cd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1d9fdfcd7bcc4f86afacc75dff5b40b77bb7b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304607"
---
# <a name="fetching-result-data"></a>提取結果資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 應用程式具備三個提取結果資料的選項。  
  
 第一個選項基於[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)。 在獲取結果集之前,應用程式使用**SQLBindCol**將結果集中的每個列綁定到程式變數。 綁定列後,驅動程式將當前行的數據傳輸到每次應用程式調用**SQLFetch**或[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)時綁定到結果集列的變數中。 如果結果集資料行和程式變數的資料類型不同，驅動程式會處理資料轉換。 如果應用程式SQL_ATTR_ROW_ARRAY_SIZE設置為大於 1,則可以將結果列綁定到變數陣列,這些變數列將在每次調用**SQLFetchScroll**時填充這些陣列。  
  
 第二個選項基於[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 應用程式不使用**SQLBindCol**將結果集列綁定到程式變數。 每次調用**SQLFetch**後,應用程式都會在結果集中的每一列調用**SQLGetData**一次。 **SQLGetData**指示驅動程式將數據從特定結果集列傳輸到特定程式變數,並指定列和變數的數據類型。 如果結果資料行和程式變數的資料類型不同，這會讓驅動程式轉換資料。 **文本****、ntext**和**圖像**列通常太大,無法放入程式變數中,但仍可以使用**SQLGetData**檢索。 如果結果列**中的文本****、ntext**或**圖像**資料大於程式變數 **,SQLGetData**將返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01004(字串數據,右截斷)。 對**SQLGetData**的連續調用返回**文本**或**圖像**數據的連續塊。 到達數據結束時 **,SQLGetData**返回SQL_SUCCESS。 如果 SQL_ATTR_ROW_ARRAY_SIZE 大於 1，每次提取都會傳回一組資料列或資料列集。 在使用**SQLGetData**之前,必須首先使用**SQLSetPos**將行集中的特定行指定為當前行。  
  
 第三個選項是使用**SQLBindCol**和**SQLGetData**的組合。 例如,應用程式可以綁定結果集的前十列,然後,每次提取時,調用**SQLGetData**三次從三個未綁定列檢索數據。 當結果集包含一個或多個**文字**或**圖像**列時,通常會使用此選項。  
  
 根據為結果集設置的游標選項,應用程式還可以使用**SQLFetchScroll**的滾動選項在結果集周圍滾動。  
  
 過度使用**SQLBindCol**將結果集列綁定到程式變數的成本很高,因為**SQLBindCol**會導致 ODBC 驅動程式分配記憶體。 將結果列綁定到變數時,該綁定將保持有效狀態,直到調用[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)以釋放語句句柄或將[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)設置為*fOption*SQL_UNBIND。 當陳述式完成時，不會自動復原繫結。  
  
 此邏輯可讓您利用不同的參數，有效地處理執行相同的 SELECT 陳述式數次。 由於結果集保持相同的結構,因此可以綁定結果集一次,處理所有 SELECT 語句,然後調用**SQLFreeStmt,fOption**設置為上次*fOption*執行後SQL_UNBIND。 如果不首先調用**SQLFreeStmt,** 則不應呼叫**SQLBindCol**將列綁定到結果集中,*而 fOption*設置為SQL_UNBIND以釋放任何以前的綁定。  
  
 使用**SQLBindCol**時,可以執行按行綁定或按列綁定。 資料列取向的繫結比資料行取向的繫結稍快。  
  
 您可以使用**SQLGetData**逐列檢索資料,而不是使用**SQLBindCol**綁定結果集列。 如果結果集僅包含幾行,則使用**SQLGetData**而不是**SQLBindCol**會更快;否則 **,SQLBindCol**可提供最佳性能。 如果不總是將數據放在同一組變數中,則應使用**SQLGetData**而不是不斷重新綁定。 只有在所有列都綁定到**SQLBindCol**後,才能在選擇清單中的列上使用**SQLGetData。** 該列還必須顯示在已使用**SQLGetData**的任何列之後。  
  
 處理將資料移至程式變數(如**SQLGetData、SQLBindCol**和[SQLBind](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)**SQLBindCol**參數 )的 ODBC 函數支援隱式資料類型轉換。 例如，如果應用程式將整數資料行繫結至字元字串程式變數，驅動程式會先自動將資料從整數轉換為字元，然後再將其放入程式變數中。  
  
 在應用程式中進行的資料轉換應該降至最低。 出非需要進行資料轉換才能讓應用程式完成處理，否則，應用程式應該將資料行和參數繫結至相同資料類型的程式變數。 不過，如果資料必須從一種類型轉換為另一種類型，讓驅動程式執行轉換比在應用程式中進行轉換還要有效率。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式一般只會直接將資料從網路緩衝區轉換到應用程式的變數。 要求驅動程式執行資料轉換會強制驅動程式緩衝處理資料，並使用 CPU 循環轉換資料。  
  
 程序變數應足夠大,以儲存從列傳輸的數據,文本 **、ntext**和**text****圖像**資料除外。 如果應用程式嘗試擷取結果集資料，並將其放入太小而無法容納它的變數中，驅動程式會產生警告。 這會強迫驅動程式為訊息配置記憶體，而且驅動程式和應用程式都必須花費 CPU 循環來處理訊息並進行錯誤處理。 應用程式應該配置夠大的變數來容納要擷取的資料，或使用選取清單中的 SUBSTRING 函數來縮減資料行在結果集中的大小。  
  
 使用 SQL_C_DEFAULT 來指定 C 變數的類型時請務必小心。 SQL_C_DEFAULT 指定 C 變數的類型必須符合資料行或參數的 SQL 資料類型。 如果為**ntext、nchar****nchar**或**nvarchar**列指定SQL_C_DEFAULT,則 Unicode 資料將返回到應用程式。 如果尚未撰寫應用程式的程式碼來處理 Unicode 資料，這可能會導致各種問題。 **唯一標識碼**(SQL_GUID) 資料類型也可能發生相同類型的問題。  
  
 **文本****、ntext**和**圖像**數據通常太大,無法放入單個程式變數中,通常使用**SQLGetData**而不是**SQLBindCol**進行處理。 使用伺服器游[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]標時,本機用戶端 ODBC 驅動程式經過優化,在提取行時不會傳輸未綁定**文本****、ntext**或**圖像**列的數據。 在應用程式為列發出**SQLGetData**之前,實際上不會從伺服器檢索**文本****、ntext**或**圖像**數據。  
  
 此優化可以應用於應用程式,以便在使用者上下滾動游標時不顯示**文本****、ntext**或**圖像**資料。 用戶選擇行后,應用程式可以調用**SQLGetData**來檢索**文本****、ntext**或**圖像**數據。 這樣可以節省使用者未選擇的任何行的傳輸**文本****、ntext**或**圖像**數據,並可以保存傳輸大量數據。  
  
## <a name="see-also"></a>另請參閱  
 [處理結果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
