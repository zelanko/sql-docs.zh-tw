---
title: "ODBC 資料表值參數的用法 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 050d0e33419b2f73fba8e5e7fd011d786fcb9f21
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="uses-of-odbc-table-valued-parameters"></a>使用 ODBC 資料表值參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主題將討論搭配 ODBC 使用資料表值參數的主要使用者案例：  
  
-   完整繫結多資料列緩衝區之下的資料表值參數 (使用記憶體中的所有值，將資料當做 TVP 傳送)  
  
-   以資料流方式傳送資料列的資料表值參數 (使用資料執行中，將資料當做 TVP 傳送)  
  
-   從系統目錄擷取資料表值參數中繼資料  
  
-   針對準備好的陳述式擷取資料表值參數中繼資料  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>完整繫結多資料列緩衝區之下的資料表值參數 (使用記憶體中的所有值，將資料當做 TVP 傳送)  
 當搭配完整繫結的多資料列緩衝區使用時，記憶體中將提供所有參數值。 例如，這對於 OLTP 交易而言就是典型的情況，在這類交易中，資料表值參數可以封裝到單一預存程序中。 如果沒有資料表值參數，這會牽涉到動態產生複雜的多重陳述式批次，或是對伺服器進行多次呼叫。  
  
 使用繫結資料表值參數本身[SQLBindParameter](http://go.microsoft.com/fwlink/?LinkId=59328)以及的其他參數。 所有參數繫都結之後，應用程式設定參數焦點屬性 SQL_SOPT_SS_PARAM_FOCUS，每個資料表值參數，而且會呼叫 SQLBindParameter 資料表值參數的資料行。  
  
 資料表值參數的伺服器類型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所特有的新類型 SQL_SS_TABLE。 SQL_SS_TABLE 的繫結 C 類型一定必須是 SQL_C_DEFAULT。 資料表值參數繫結的參數不會傳送任何資料；它是用來傳遞資料表中繼資料，以及控制要如何傳遞資料表值參數之組成資料行中的資料。  
  
 資料表值參數的長度會設定為傳送給伺服器的資料列數。 *ColumnSize* SQLBindParameter 參數是資料表值參數會指定可以傳送的資料列的數目上限，這是資料行緩衝區的陣列大小。 *ParameterValuePtr*是 SQLBindParameter 中資料表值參數的參數緩衝區。 *ParameterValuePtr*及其相關聯*Columnsize*用來傳遞資料表值參數時所需的型別名稱。 此類型名稱不是預存程序呼叫所需，但為 SQL 陳述式所需。  
  
 SQLBindParameter 的呼叫上指定資料表值參數類型名稱時，它必須永遠指定為 Unicode 值，即使在建置為 ANSI 應用程式的應用程式。 當您使用 SQLSetDescField 指定資料表值參數的型別名稱時，您可以使用符合應用程式建置方式的常值。 ODBC 驅動程式管理員將會執行所有必要的 Unicode 轉換。  
  
 資料表值參數和資料表值參數資料行的中繼資料可以明確及個別操作使用 SQLGetDescRec、 SQLSetDescRec、 SQLGetDescField 和 SQLSetDescField。 不過，多載 SQLBindParameter 通常更方便且不需要明確描述項存取，在大部分情況下。 這個方法是與其他資料類型，SQLBindParameter 定義一致，只不過是資料表值參數的受影響的描述項欄位有些許不同。  
  
 有時應用程式會搭配動態 SQL 使用資料表值參數，而且必須提供此資料表值參數的類型名稱。 如果是這樣，連接的目前預設結構描述中未定義的資料表值參數使用 SQLSetDescField 必須設定 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME。 因為資料表類型定義和資料表值參數必須在相同的資料庫中，所以如果應用程式使用資料表值參數，就不能設定 SQL_CA_SS_TYPE_CATALOG_NAME。 否則，SQLSetDescField 會回報錯誤。  
  
 在此案例的範例程式碼是在程序`demo_fixed_TVP_binding`中[使用資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>以資料流方式傳送資料列的資料表值參數 (使用資料執行中，將資料當做 TVP 傳送)  
 在此案例中，應用程式會在要求時提供資料列給驅動程式，然後以資料流方式將資料列傳送給伺服器。 如此就不需要在記憶體中緩衝處理所有資料列。 這是大量插入/更新案例的代表。 資料表值參數會提供參數陣列與大量複製之間某一處的效能點。 也就是說，編寫資料表值參數就跟參數陣列一樣輕鬆，但是資料表值參數在伺服器上提供更大的彈性。  
  
 如同上一節「完整繫結多資料列緩衝區之下的資料表值參數」所討論，資料表值參數和它的資料行會繫結在一起，但是資料表值參數本身的長度指標會設定為 SQL_DATA_AT_EXEC。 資料在執行中參數的一般方式在驅動程式會回應 SQLExecute 或 SQLExecuteDirect — 也就是藉由傳回 SQL_NEED_DATA。 SQLParamData 驅動程式準備好要接受資料表值參數的資料時，傳回的值*ParameterValuePtr* SQLBindParameter 中。  
  
 應用程式會使用資料表值參數的 SQLPutData，表示資料表值參數組成資料行的資料可用性。 針對資料表值參數，呼叫 SQLPutData 時*DataPtr*必須一律為 null 和*StrLen_or_Ind*必須是 0 或數字小於或等於指定的陣列大小資料表值參數緩衝區 ( *ColumnSize* SQLBindParameter 參數)。 0 表示資料表值參數沒有其他資料列，而且此驅動程式將會繼續處理下一個實際程序參數。 當*StrLen_or_Ind*是不是 0，此驅動程式會處理資料表值參數組成資料行相同的方式為非資料表值參數繫結參數： 每個資料表值參數資料行可以指定其實際的資料長度、 SQL_NULL_DATA，或它可以指定在執行透過其長度/指標緩衝區的資料。 資料表值參數資料行的值可以傳像往常一樣重複呼叫 SQLPutData，要以片段傳遞字元或二進位值時。  
  
 當所有資料表值參數資料行都已經處理過之後，此驅動程式會回到資料表值參數來進一步處理資料表值參數資料的資料列。 因此，如果是資料執行中的資料表值參數，此驅動程式不會遵循一般的繫結參數循序掃描。 將會輪詢繫結的資料表值參數，直到呼叫是 SQLPutData *StrLen_Or_IndPtr*等於 0，此時驅動程式略過資料表值參數資料行，並移至下一個實際預存程序參數。  當 SQLPutData 傳指標值大於或等於 1 時，驅動程式處理資料表值參數資料行和資料列依序直到它有所有的繫結的資料列和資料行的值。 然後此驅動程式會回到資料表值參數。 之間接收資料表值參數的語彙基元從 SQLParamData 和 SQLPutData (hstmt，NULL，n) 呼叫資料表值參數，應用程式必須設定資料表值參數組成資料行資料和指標緩衝區的內容。下一個資料列或資料列傳遞至伺服器。  
  
 在此案例的範例程式碼位於常式`demo_variable_TVP_binding`中[使用資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>從系統目錄擷取資料表值參數中繼資料  
 當應用程式具有資料表值參數的程序呼叫 SQLProcedureColumns 時，DATA_TYPE 會以 SQL_SS_TABLE 而且 TYPE_NAME 是資料表值參數資料表類型的名稱傳回。 SQLProcedureColumns 傳回的結果集已加入兩個額外的資料行： SS_TYPE_CATALOG_NAME 會傳回定義資料表類型之資料表值參數，而 SS_TYPE_SCHEMA_NAME 會傳回的結構描述名稱的目錄名稱位置定義資料表類型的資料表值參數的位置。 依照 ODBC 規格規定，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 會出現在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所加入的所有驅動程式特有資料行之前，以及 ODBC 本身所託管的所有資料行之後。  
  
 新的資料行不但會針對資料表值參數擴展，也會針對 CLR 使用者定義型別參數擴展。 仍然會擴展 UDT 參數現有的結構描述和目錄資料行，但是讓需要的資料類型擁有共同的結構描述和目錄資料行將會簡化未來的應用程式開發過程  (請注意，XML 結構描述集合會有些不同，而且未包含在這項變更中)。  
  
 應用程式會使用 SQLTables，它會保存的資料表、 系統資料表和檢視表的相同方式決定資料表類型的名稱。 新的資料表類型 TABLE TYPE 已經導入，可讓應用程式識別與資料表值參數相關聯的資料表類型。 資料表類型和一般表格會使用不同的命名空間。 這表示，您可以將相同的名稱用於資料表類型和實際資料表。 為了處理這個情況，已經導入了新的陳述式屬性 SQL_SOPT_SS_NAME_SCOPE。 這個屬性會指定是否 SQLTables 和其他採用資料表做為參數名稱的目錄函數應該解譯資料表名稱做為實際的資料表名稱或資料表類型的名稱。  
  
 應用程式使用 SQLColumns 中保存的資料表，但必須先設定 SQL_SOPT_SS_NAME_SCOPE 來指示它使用資料表類型，而不是實際資料表的相同方式決定資料表類型的資料行。 SQLPrimaryKeys 也可以搭配資料表類型，再利用 SQL_SOPT_SS_NAME_SCOPE。  
  
 在此案例的範例程式碼位於常式`demo_metadata_from_catalog_APIs`中[使用資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>針對準備好的陳述式擷取資料表值參數中繼資料  
 在此案例中，應用程式會使用 SQLNumParameters 和 SQLDescribeParam 擷取資料表值參數的中繼資料。  
  
 IPD 欄位 SQL_CA_SS_TYPE_NAME 是用來擷取資料表值參數的類型名稱。 IPD 欄位 SQL_CA_SS_TYPE_SCHEMA_NAME 和 SQL_CA_SS_TYPE_CATALOG_NAME 是分別用來擷取它的目錄和結構描述。  
  
 資料表類型定義和資料表值參數必須在相同的資料庫中。 如果應用程式在使用資料表值參數時設定 SQL_CA_SS_TYPE_CATALOG_NAME SQLSetDescField 會報告錯誤。  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 也可以用來擷取與 CLR 使用者定義型別參數相關聯的目錄和結構描述。 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 是 CLR UDT 類型的現有類型特有之目錄結構描述屬性的替代方式。  
  
 應用程式使用 SQLColumns 擷取資料行中繼資料資料表值參數在此案例中，也因為 SQLDescribeParam 不會傳回資料表值參數資料行的資料行的中繼資料。  
  
 此使用案例的範例程式碼位於常式`demo_metadata_from_prepared_statement`中[使用資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
