---
title: 資料表值參數描述項欄位 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields
ms.assetid: 4e009eff-c156-4d63-abcf-082ddd304de2
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6205ed15e0771cc1900a458343defbbcb0e1384f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32946513"
---
# <a name="table-valued-parameter-descriptor-fields"></a>資料表值參數描述項欄位
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  資料表值參數的支援包含 ODBC 應用程式參數描述項 (APD) 和實作參數描述項 (IPD) 中新增的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定欄位。  
  
## <a name="remarks"></a>備註  
  
|名稱|位置|型別|Description|  
|----------|--------------|----------|-----------------|  
|SQL_CA_SS_TYPE_NAME|IPD|SQLTCHAR *|資料表值參數的伺服器類型名稱。<br /><br /> SQLBindParameter 的呼叫上指定資料表值參數類型名稱時，它必須永遠指定為 Unicode 值，即使在建置為 ANSI 應用程式的應用程式。 用於參數的值*StrLen_or_IndPtr*應該是 SQL_NTS 或是字串長度乘以 sizeof （wchar） 的名稱。<br /><br /> 當資料表值參數類型名稱透過指定 SQLSetDescField，它可以使用指定的常值與應用程式一致的方式，是所建立。 ODBC 驅動程式管理員將會執行所有必要的 Unicode 轉換。|  
|SQL_CA_SS_TYPE_CATALOG_NAME (唯讀)|IPD|SQLTCHAR *|類型定義所在的目錄。|  
|SQL_CA_SS_TYPE_SCHEMA_NAME|IPD|SQLTCHAR *|類型定義所在的結構描述。|  
  
 應用程式不得針對資料表值參數設定 SQL_CA_SS_TYPE_CATALOG_NAME。 這麼做會傳回 SQL_ERROR，而且會記錄具有 SQLSTATE=HY091 和「無效的描述項欄位識別碼」訊息的診斷記錄。  
  
 當參數焦點設定為資料表值參數時，資料表值參數適用下列的陳述式屬性和描述項標頭欄位：  
  
|名稱|位置|型別|Description|  
|----------|--------------|----------|-----------------|  
|SQL_ATTR_PARAMSET_SIZE<br /><br /> (這相當於在 APD 中的 SQL_DESC_ARRAY_SIZE)。|APD|SQLUINTEGER|資料表值參數的緩衝區陣列的陣列大小。 這是緩衝區可容納的最大資料列數目，或者以資料列表示的緩衝區大小；資料表值參數值本身的資料列可能多於或少於緩衝區所能保存的資料列。 預設值為 1。<br /><br /> 注意： 如果 SQL_SOPT_SS_PARAM_FOCUS 設定為其預設值為 0，則 sql_attr_paramset_size 會參考陳述式，並指定的參數集數目。 如果 SQL_SOPT_SS_PARAM_FOCUS 設定為資料表值參數的序數，則它會參考資料表值參數並針對資料表值參數而指定每個參數集的資料列數。|  
|SQL_ATTR_PARAM _BIND_TYPE|APD|SQLINTEGER|預設值為 SQL_PARAM_BIND_BY_COLUMN。<br /><br /> 若要選取資料列繫結，這個欄位會設定為會繫結到資料表值參數資料列集之結構或緩衝區執行個體的長度。 這個長度會包含所有繫結資料行以及結構或緩衝區之任何填補的空間。 如此可確保在使用指定長度遞增繫結資料行的位址時，結果會指向下一個資料列中相同資料行的起始處。 當使用**sizeof** ANSI C 中的運算子，保證此行為。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|APD|SQLINTEGER*|預設值為 Null 指標。<br /><br /> 如果此欄位非 Null，則驅動程式會取消指標的參考、將取消參考的值加入至描述項記錄中的每個延遲欄位 (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR)，然後使用新的指標值來存取資料值。|  
  
 這些欄位只有在使用資料表值參數時才有效，其他的資料類型會加以忽略。  
  
 SQL_CA_SS_TYPE_NAME 對預存程序呼叫而言是選擇性的。 必須針對不是程序呼叫的 SQL 陳述式指定這個欄位，才能讓伺服器判斷資料表值參數的類型。  
  
 如果需要類型名稱，且資料表值參數的資料表類型是定義於預存程序以外的結構描述中，則必須在實作參數描述項 (IPD) 中指定 SQL_CA_SS_TYPE_SCHEMA_NAME。 如果沒有指定，伺服器將無法判斷資料表值參數的類型。 當您呼叫 SQLExecute 或 SQLExecDirect 時，這會導致錯誤。 錯誤將具有 SQLSTATE= 07006 和訊息「限制的資料類型屬性違規」。  
  
 資料表值參數資料行可以使用資料列繫結或資料行繫結。 預設為資料行繫結。 資料列繫結可以藉由設定 SQL_ATTR_PARAM_BIND_TYPE 和 SQL_ATTR_ PARAM_BIND_OFFSET_PTR 來指定。 這與資料行和參數的資料列繫結類似。  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 也可以用來擷取與 CLR 使用者定義型別參數相關聯的目錄和結構描述。 這些欄位是這些類型現有之類型特定目錄結構描述屬性的替代項目。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
