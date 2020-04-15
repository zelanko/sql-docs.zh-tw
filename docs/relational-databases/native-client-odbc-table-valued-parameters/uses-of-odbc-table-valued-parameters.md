---
title: ODBC 表值參數的使用 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e88092c6566d9e5838f8a2cb59cd7c23564af9b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297731"
---
# <a name="uses-of-odbc-table-valued-parameters"></a>使用 ODBC 資料表值參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題將討論搭配 ODBC 使用資料表值參數的主要使用者案例：  
  
-   完整繫結多資料列緩衝區之下的資料表值參數 (使用記憶體中的所有值，將資料當做 TVP 傳送)  
  
-   以資料流方式傳送資料列的資料表值參數 (使用資料執行中，將資料當做 TVP 傳送)  
  
-   從系統目錄擷取資料表值參數中繼資料  
  
-   針對準備好的陳述式擷取資料表值參數中繼資料  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>完整繫結多資料列緩衝區之下的資料表值參數 (使用記憶體中的所有值，將資料當做 TVP 傳送)  
 當搭配完整繫結的多資料列緩衝區使用時，記憶體中將提供所有參數值。 例如，這對於 OLTP 交易而言就是典型的情況，在這類交易中，資料表值參數可以封裝到單一預存程序中。 如果沒有資料表值參數，這會牽涉到動態產生複雜的多重陳述式批次，或是對伺服器進行多次呼叫。  
  
 表值參數本身通過使用[SQLBind 參數](https://go.microsoft.com/fwlink/?LinkId=59328)和其他參數綁定。 綁定完所有參數後,應用程式將參數焦點屬性SQL_SOPT_SS_PARAM_FOCUS在每個表值參數上設置,並調用 SQLBindparameter 作為表值參數的列。  
  
 資料表值參數的伺服器類型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所特有的新類型 SQL_SS_TABLE。 SQL_SS_TABLE 的繫結 C 類型一定必須是 SQL_C_DEFAULT。 資料表值參數繫結的參數不會傳送任何資料；它是用來傳遞資料表中繼資料，以及控制要如何傳遞資料表值參數之組成資料行中的資料。  
  
 資料表值參數的長度會設定為傳送給伺服器的資料列數。 表值參數的 SQLBind 參數的*欄大小*參數指定可發送的最大行數;這是列緩衝區的陣列大小。 *參數ValuePtr*是 SQLBind 參數中表值參數的參數緩衝區。 *參數ValuePtr*及其關聯的*緩衝區長度*用於在需要時傳遞表值參數的類型名稱。 此類型名稱不是預存程序呼叫所需，但為 SQL 陳述式所需。  
  
 當在調用 SQLBindParameter 時指定表值參數類型名稱時,必須始終將其指定為 Unicode 值,即使在構建為 ANSI 應用程式的應用程式中也是如此。 使用 SQLSetDescField 指定表值參數類型名稱時,可以使用符合應用程式生成方式的文本。 ODBC 驅動程式管理員將會執行所有必要的 Unicode 轉換。  
  
 通過使用 SQLGetDescRec、SQLSetDescRec、SQLGetDescField 和 SQLSetDescField,可以單獨和顯式地操作表值參數和表值參數列的元數據。 但是,重載 SQLBind 參數通常更方便,在大多數情況下不需要顯式描述符訪問。 此方法與其他數據類型的 SQLBindParameter 定義一致,只不過對於表值參數,受影響的描述符位略有不同。  
  
 有時應用程式會搭配動態 SQL 使用資料表值參數，而且必須提供此資料表值參數的類型名稱。 如果是這種情況,並且未在連接的當前預設架構中定義表值參數,則必須使用 SQLSetDescField 設置SQL_CA_SS_TYPE_CATALOG_NAME和SQL_CA_SS_TYPE_SCHEMA_NAME。 因為資料表類型定義和資料表值參數必須在相同的資料庫中，所以如果應用程式使用資料表值參數，就不能設定 SQL_CA_SS_TYPE_CATALOG_NAME。 否則,SQLSetDescField 將報告錯誤。  
  
 這個機制的範例碼在`demo_fixed_TVP_binding`[使用表值參數&#40;ODBC&#41;中](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>以資料流方式傳送資料列的資料表值參數 (使用資料執行中，將資料當做 TVP 傳送)  
 在此案例中，應用程式會在要求時提供資料列給驅動程式，然後以資料流方式將資料列傳送給伺服器。 如此就不需要在記憶體中緩衝處理所有資料列。 這是大量插入/更新案例的代表。 資料表值參數會提供參數陣列與大量複製之間某一處的效能點。 也就是說，編寫資料表值參數就跟參數陣列一樣輕鬆，但是資料表值參數在伺服器上提供更大的彈性。  
  
 如同上一節「完整繫結多資料列緩衝區之下的資料表值參數」所討論，資料表值參數和它的資料行會繫結在一起，但是資料表值參數本身的長度指標會設定為 SQL_DATA_AT_EXEC。 驅動程式以執行時資料參數的通常方式回應 SQLExecute 或 SQLExecuteDirect,即返回SQL_NEED_DATA。 當驅動程式準備好接受表值參數的數據時,SQLParamData 將返回 SQLBind 參數中的*參數ValuePtr*的值。  
  
 應用程式使用 SQLPutData 作為表值參數來指示表值參數組成列的數據的可用性。 當為表值參數呼叫 SQLPutData 時 *,DataPtr*必須始終為空,*並且StrLen_or_Ind*必須為小於或等於為表值緩衝區指定的陣列大小(SQLBind參數的*列大小*參數)的數位。 0 表示資料表值參數沒有其他資料列，而且此驅動程式將會繼續處理下一個實際程序參數。 當*StrLen_or_Ind*不是 0 時,驅動程式將以與非表值參數綁定參數相同的方式處理表值參數組成列:每個表值參數列可以指定其實際數據長度、SQL_NULL_DATA,或者可以通過其長度/指示器緩衝區指定執行時的數據。 當字元或二進位值分段傳遞時,可以通過像往常一樣重複調用 SQLPutData 來傳遞表值參數列值。  
  
 當所有資料表值參數資料行都已經處理過之後，此驅動程式會回到資料表值參數來進一步處理資料表值參數資料的資料列。 因此，如果是資料執行中的資料表值參數，此驅動程式不會遵循一般的繫結參數循序掃描。 將輪詢綁定的表值參數,直到將 SQLPutData 調用*StrLen_Or_IndPtr*等於 0,此時驅動程式將跳過表值參數列並移動到下一個實際存儲過程參數。  當 SQLPutData 傳遞大於或等於 1 的指標值時,驅動程式會按順序處理表值參數列和行,直到它具有所有綁定行和列的值。 然後此驅動程式會回到資料表值參數。 從 SQLParamData 接收表值參數的權杖和為表值參數呼叫 SQLPutData(hstmt、NULL、n)之間,應用程式必須設定表值參數組成列資料和指示器緩衝區內容,以便下一行或行傳遞給伺服器。  
  
 此方案的範例代碼在`demo_variable_TVP_binding`[使用表值參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)中的例程中。  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>從系統目錄擷取資料表值參數中繼資料  
 當應用程式為具有表值參數的過程調用 SQLAKK 時,DATA_TYPE將作為SQL_SS_TABLE返回,TYPE_NAME是表值參數的表類型的名稱。 向 SQLAAK 傳回的結果集添加了兩個其他列:SS_TYPE_CATALOG_NAME返回定義表值參數的表類型的目錄的名稱,SS_TYPE_SCHEMA_NAME返回定義表值參數的表類型的架構的名稱。 依照 ODBC 規格規定，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 會出現在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所加入的所有驅動程式特有資料行之前，以及 ODBC 本身所託管的所有資料行之後。  
  
 新的資料行不但會針對資料表值參數擴展，也會針對 CLR 使用者定義型別參數擴展。 仍然會擴展 UDT 參數現有的結構描述和目錄資料行，但是讓需要的資料類型擁有共同的結構描述和目錄資料行將會簡化未來的應用程式開發過程  (請注意，XML 結構描述集合會有些不同，而且未包含在這項變更中)。  
  
 應用程式使用 SQLTables 確定表類型的名稱與對持久表、系統表和檢視的名稱相同。 新的資料表類型 TABLE TYPE 已經導入，可讓應用程式識別與資料表值參數相關聯的資料表類型。 資料表類型和一般表格會使用不同的命名空間。 這表示，您可以將相同的名稱用於資料表類型和實際資料表。 為了處理這個情況，已經導入了新的陳述式屬性 SQL_SOPT_SS_NAME_SCOPE。 此屬性指定 SQLTables 和將表名稱作為參數的其他目錄函數是否應將表名稱解釋為實際表的名稱或表類型的名稱。  
  
 應用程式使用 SQLColumns 以與持久表相同的方式確定表類型的列,但必須首先SQL_SOPT_SS_NAME_SCOPE設置以指示它正在使用表類型而不是實際表。 SQL主要密鑰也可以與表類型一起使用,再次使用SQL_SOPT_SS_NAME_SCOPE。  
  
 此方案的範例代碼在`demo_metadata_from_catalog_APIs`[使用表值參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)中的例程中。  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>針對準備好的陳述式擷取資料表值參數中繼資料  
 在這種情況下,應用程式使用 SQLNum 參數和 SQLDescribeParam 檢索表值參數的中繼資料。  
  
 IPD 欄位 SQL_CA_SS_TYPE_NAME 是用來擷取資料表值參數的類型名稱。 IPD 欄位 SQL_CA_SS_TYPE_SCHEMA_NAME 和 SQL_CA_SS_TYPE_CATALOG_NAME 是分別用來擷取它的目錄和結構描述。  
  
 資料表類型定義和資料表值參數必須在相同的資料庫中。 如果應用程式在使用表值參數時設置SQL_CA_SS_TYPE_CATALOG_NAME,SQLSetDescField 將報告錯誤。  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 也可以用來擷取與 CLR 使用者定義型別參數相關聯的目錄和結構描述。 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 是 CLR UDT 類型的現有類型特有之目錄結構描述屬性的替代方式。  
  
 在這種情況下,應用程式也使用 SQLColumn 檢索表值參數的列元數據,因為 SQLDescribeParam 不會返回表值參數列的列的中繼資料。  
  
 此用例的範例代碼在`demo_metadata_from_prepared_statement`[使用表值參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)中的例程中。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
