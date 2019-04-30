---
title: 提取結果資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b803ca3742f9cb831e51105aab9d0ed75ad78e16
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200078"
---
# <a name="fetching-result-data"></a>提取結果資料
  ODBC 應用程式具備三個提取結果資料的選項。  
  
 第一個選項根據[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)。 應用程式提取結果集之前，請使用**SQLBindCol**中結果集至程式變數繫結每個資料行。 驅動程式會將目前的資料列，為變數的資料繫結至結果集資料行每個資料行都已繫結之後，時間應用程式會呼叫**SQLFetch**或是[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)。 如果結果集資料行和程式變數的資料類型不同，驅動程式會處理資料轉換。 如果應用程式將 sql_attr_row_array_size 設定為大於 1，它可以繫結結果資料行至變數，在每次呼叫會先填入陣列**SQLFetchScroll**。  
  
 第二個選項根據[SQLGetData](../native-client-odbc-api/sqlgetdata.md)。 應用程式不會使用**SQLBindCol**繫結結果集資料行至程式變數。 在每次呼叫之後**SQLFetch**，應用程式會呼叫**SQLGetData**一次的結果中的每個資料行設定。 **SQLGetData**指示將從特定的結果集資料行的資料傳送到特定的程式變數的驅動程式，並指定資料行和變數的資料類型。 如果結果資料行和程式變數的資料類型不同，這會讓驅動程式轉換資料。 **文字**， **ntext**，以及**映像**資料行通常太大而無法容納到程式變數，但仍可使用擷取**SQLGetData**。 如果**文字**， **ntext**，或**映像**結果資料行中的資料大於程式變數， **SQLGetData**傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （字串資料，右邊已截斷）。 後續呼叫**SQLGetData**會傳回連續區塊**文字**或是**映像**資料。 當到達資料的結尾時， **SQLGetData**都會傳回 SQL_SUCCESS。 如果 SQL_ATTR_ROW_ARRAY_SIZE 大於 1，每次提取都會傳回一組資料列或資料列集。 使用之前**SQLGetData**，您必須先使用**SQLSetPos**指定為目前的資料列的特定資料列集中的資料列。  
  
 第三個選項是使用混合**SQLBindCol**並**SQLGetData**。 應用程式無法比方說，繫結結果集的前十個資料行，然後每回擷取時，呼叫**SQLGetData**三次，以從三個未繫結的資料行擷取資料。 通常會使用此法時的結果集包含一或多個**文字**或是**映像**資料行。  
  
 根據結果集的資料指標選項，應用程式也可以使用的捲動選項**SQLFetchScroll**來捲動結果集。  
  
 過度使用**SQLBindCol**繫結結果集資料行至程式變數是昂貴因為**SQLBindCol**會導致配置記憶體的 ODBC 驅動程式。 當您將結果資料行繫結至變數時，該繫結會持續有效，直到您呼叫[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)來釋放陳述式控制代碼或呼叫[SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md)使用*fOption*設定為 SQL_UNBIND。 當陳述式完成時，不會自動復原繫結。  
  
 此邏輯可讓您利用不同的參數，有效地處理執行相同的 SELECT 陳述式數次。 結果集會保留相同的結構，因為您可以將繫結結果集一次，處理所有 SELECT 陳述式，然後呼叫**SQLFreeStmt**具有*fOption*設定為 SQL_UNBIND 之後上一次執行。 您不應該呼叫**SQLBindCol**繫結結果集，而不需第一個呼叫中的資料行**SQLFreeStmt**具有*fOption*設定為 SQL_UNBIND，以釋放先前所有繫結。  
  
 使用時**SQLBindCol**，您可以進行資料列取向或資料行取向的繫結。 資料列取向的繫結比資料行取向的繫結稍快。  
  
 您可以使用**SQLGetData**擷取資料的逐欄為基礎，而不是繫結結果集使用的資料行**SQLBindCol**。 如果結果集只包含少數資料列，使用**SQLGetData**而不是**SQLBindCol**更快，否則**SQLBindCol**提供最佳的效能。 如果您不在相同的變數集合中一律將資料，您應該使用**SQLGetData**而非不斷重新繫結。 您只能使用**SQLGetData**資料行上的選取清單中的所有資料行使用繫結之後**SQLBindCol**。 資料行也必須出現在其您已經使用任何資料行後面**SQLGetData**。  
  
 ODBC 函式，來處理，例如將資料移入或移出程式變數**SQLGetData**， **SQLBindCol**，並[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)，支援隱含的資料類型轉換。 例如，如果應用程式將整數資料行繫結至字元字串程式變數，驅動程式會先自動將資料從整數轉換為字元，然後再將其放入程式變數中。  
  
 在應用程式中進行的資料轉換應該降至最低。 出非需要進行資料轉換才能讓應用程式完成處理，否則，應用程式應該將資料行和參數繫結至相同資料類型的程式變數。 不過，如果資料必須從一種類型轉換為另一種類型，讓驅動程式執行轉換比在應用程式中進行轉換還要有效率。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式一般只會直接將資料從網路緩衝區轉換到應用程式的變數。 要求驅動程式執行資料轉換會強制驅動程式緩衝處理資料，並使用 CPU 循環轉換資料。  
  
 程式變數要夠大，無法保存資料傳輸中資料行，除了**文字**， **ntext**，並**映像**資料。 如果應用程式嘗試擷取結果集資料，並將其放入太小而無法容納它的變數中，驅動程式會產生警告。 這會強迫驅動程式為訊息配置記憶體，而且驅動程式和應用程式都必須花費 CPU 循環來處理訊息並進行錯誤處理。 應用程式應該配置夠大的變數來容納要擷取的資料，或使用選取清單中的 SUBSTRING 函數來縮減資料行在結果集中的大小。  
  
 使用 SQL_C_DEFAULT 來指定 C 變數的類型時請務必小心。 SQL_C_DEFAULT 指定 C 變數的類型必須符合資料行或參數的 SQL 資料類型。 如果指定 SQL_C_DEFAULT **ntext**， **nchar**，或**nvarchar**  欄中，Unicode 資料會傳回到應用程式。 如果尚未撰寫應用程式的程式碼來處理 Unicode 資料，這可能會導致各種問題。 相同類型的問題可能會發生**uniqueidentifier** (SQL_GUID) 資料型別。  
  
 **文字**， **ntext**，以及**映像**資料通常是太大而無法放入單一程式變數，並且通常處理具有**SQLGetData**而不是**SQLBindCol**。 使用伺服器資料指標，當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式已最佳化，不傳送未繫結資料**文字**， **ntext**，或**映像**於資料行擷取資料列的時間。 **文字**， **ntext**，或**映像**不會實際擷取資料從伺服器應用程式問題直到**SQLGetData**的資料行。  
  
 此最佳化可以套用至應用程式，讓沒有**文字**， **ntext**，或**映像**使用者游標上下捲動時，會顯示資料。 在使用者選取一個資料列之後，應用程式可以呼叫**SQLGetData**來擷取**文字**， **ntext**，或**映像**資料。 這樣就不用傳送**文字**， **ntext**，或**映像**的任何資料列的資料不會選取使用者和也不用傳送非常大量的資料。  
  
## <a name="see-also"></a>另請參閱  
 [處理結果&#40;ODBC&#41;](processing-results-odbc.md)  
  
  
