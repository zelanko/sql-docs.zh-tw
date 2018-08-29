---
title: 資料表值參數 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC)
- ODBC, table-valued parameters
ms.assetid: ef06cd13-18e2-4c65-8ede-c3955d820e54
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 69a87a556e9deb8fb94138112822be7bf99ec8d0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43070181"
---
# <a name="table-valued-parameters-odbc"></a>資料表值參數 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 對資料表值參數的支援可讓用戶端應用程式有效率地將參數化資料傳送給伺服器，其方式是使用一個呼叫來傳送多個資料列給伺服器。  
  
 如需資料表值參數在伺服器上的資訊，請參閱[使用資料表值參數&#40;資料庫引擎&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
 在 ODBC 中，這是您可以將資料表值參數傳送給伺服器的兩種方式：  
  
-   SQLExecDirect 或 SQLExecute 呼叫時，所有資料表值參數資料可以都是在記憶體中。 如果資料表值中有多個資料列，這些資料會儲存在陣列中。  
  
-   SQLExecDirect 或 SQLExecute 呼叫時，應用程式可以指定資料執行的是資料表值參數。 在此情況下，可以在批次中提供資料表值的資料列，或是一次一個來減少記憶體需求。  
  
 第一個選項可讓預存程序封裝更多商務邏輯。 例如，將其他項目當做資料表值參數傳遞時，單一預存程序可封裝整個訂單輸入交易。 這個選項非常有效率，因為只需要單一次往返伺服器。 另外，您也可以使用不同程序來個別處理訂單標頭和訂單項目，這樣需要在用戶端與伺服器之間有更多的程式碼和更複雜的合約。  
  
 第二個方法針對具有極大量資料的大量作業提供了一種有效率的機制。 這可讓應用程式以資料流方式將資料列傳送到伺服器，而不必先在記憶體中緩衝處理所有的資料。  
  
 當您建立資料表變數時，可以建立條件約束和主索引鍵。 條件約束是確保資料表中的資料符合特定需求的一種很好方式。  
  
## <a name="in-this-section"></a>本節內容  
 [使用 ODBC 資料表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/uses-of-odbc-table-valued-parameters.md)  
 描述資料表值參數和 ODBC 的主要使用者案例。  
  
 [資料表值參數的 ODBC SQL 類型](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-sql-type-for-table-valued-parameters.md)  
 描述 SQL_SS_TABLE 類型。 這是可支援資料表值參數的新 ODBC SQL 類型。  
  
 [資料表值參數描述項欄位](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)  
 描述可支援資料表值參數的描述項欄位。  
  
 [資料表值參數組成資料行的描述項欄位](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)  
 描述對於資料表值參數具有意義的描述項欄位。  
  
 [資料表值參數診斷記錄欄位](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-diagnostic-record-fields.md)  
 描述已經加入到診斷記錄中來支援資料表值參數的兩個診斷欄位。  
  
 [影響資料表值參數的陳述式屬性](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)  
 描述可讓資料表值參數資料行得以處理的新描述項標頭欄位。  
  
 [資料表值參數和資料行值的繫結與資料傳送](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)  
 描述參數繫結以及如何將資料表值參數傳遞給伺服器。  
  
 [已備妥之陳述式的資料表值參數中繼資料](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)  
 描述應用程式要如何針對預備好的程序呼叫取得中繼資料。  
  
 [其他資料表值參數中繼資料](../../relational-databases/native-client-odbc-table-valued-parameters/additional-table-valued-parameter-metadata.md)  
 描述如何使用 SQLProcedureColumns、 SQLTables 和 SQLColumns 擷取的資料表值參數的中繼資料。  
  
 [資料表值參數資料轉換及其他錯誤和警告](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-data-conversion-and-other-errors-and-warnings.md)  
 描述如何處理有關資料表值參數資料行值的錯誤。  
  
 [跨版本相容性](../../relational-databases/native-client-odbc-table-valued-parameters/cross-version-compatibility.md)  
 描述當早於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本的用戶端或伺服器使用資料表值參數時，可能發生的衝突。  
  
 [ODBC 資料表值參數 API 摘要](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-table-valued-parameter-api-summary.md)  
 列出可支援資料表值參數的 ODBC 函數。  
  
 [ODBC 資料表值參數程式設計範例](http://msdn.microsoft.com/library/3f52b7a7-f2bd-4455-b79e-d015fb397726)  
 描述如何執行一般工作。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [資料表值參數&#40;SQL Server Native Client&#41;](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
  
  
