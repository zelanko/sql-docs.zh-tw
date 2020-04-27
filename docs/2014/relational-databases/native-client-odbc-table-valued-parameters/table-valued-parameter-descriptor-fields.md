---
title: 資料表值參數描述項欄位 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields
ms.assetid: 4e009eff-c156-4d63-abcf-082ddd304de2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd58bdb611a070c812364baf2fa3e1544c2ffdc9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63228960"
---
# <a name="table-valued-parameter-descriptor-fields"></a>資料表值參數描述項欄位
  資料表值參數的支援包含 ODBC 應用程式參數描述項 (APD) 和實作參數描述項 (IPD) 中新增的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定欄位。  
  
## <a name="remarks"></a>備註  
  
|名稱|位置|類型|描述|  
|----------|--------------|----------|-----------------|  
|SQL_CA_SS_TYPE_NAME|IPD|SQLTCHAR *|資料表值參數的伺服器類型名稱。<br /><br /> 當資料表值參數類型名稱是在呼叫 SQLBindParameter 時指定時，一定要將它指定為 Unicode 值，即使在以 ANSI 應用程式形式建立的應用程式中也是如此。 參數*StrLen_or_IndPtr*所使用的值應該是 SQL_NTS 或名稱的字串長度乘以 SIZEOF （WCHAR）。<br /><br /> 透過 SQLSetDescField 指定資料表值參數類型名稱時，可以使用符合應用程式建立方式的常值來指定。 ODBC 驅動程式管理員將會執行所有必要的 Unicode 轉換。|  
|SQL_CA_SS_TYPE_CATALOG_NAME (唯讀)|IPD|SQLTCHAR *|類型定義所在的目錄。|  
|SQL_CA_SS_TYPE_SCHEMA_NAME|IPD|SQLTCHAR *|類型定義所在的結構描述。|  
  
 應用程式不得針對資料表值參數設定 SQL_CA_SS_TYPE_CATALOG_NAME。 這麼做會傳回 SQL_ERROR，而且會記錄具有 SQLSTATE=HY091 和「無效的描述項欄位識別碼」訊息的診斷記錄。  
  
 當參數焦點設定為資料表值參數時，資料表值參數適用下列的陳述式屬性和描述項標頭欄位：  
  
|名稱|位置|類型|描述|  
|----------|--------------|----------|-----------------|  
|SQL_ATTR_PARAMSET_SIZE<br /><br /> (這相當於在 APD 中的 SQL_DESC_ARRAY_SIZE)。|APD|SQLUINTEGER|資料表值參數的緩衝區陣列的陣列大小。 這是緩衝區可容納的最大資料列數目，或者以資料列表示的緩衝區大小；資料表值參數值本身的資料列可能多於或少於緩衝區所能保存的資料列。 預設值為 1。 **注意：** 如果 SQL_SOPT_SS_PARAM_FOCUS 設定為預設值0，SQL_ATTR_PARAMSET_SIZE 會參考語句並指定參數集的數目。 如果 SQL_SOPT_SS_PARAM_FOCUS 設定為資料表值參數的序數，則它會參考資料表值參數並針對資料表值參數而指定每個參數集的資料列數。|  
|SQL_ATTR_PARAM _BIND_TYPE|APD|SQLINTEGER|預設值為 SQL_PARAM_BIND_BY_COLUMN。<br /><br /> 若要選取資料列繫結，這個欄位會設定為會繫結到資料表值參數資料列集之結構或緩衝區執行個體的長度。 這個長度會包含所有繫結資料行以及結構或緩衝區之任何填補的空間。 如此可確保在使用指定長度遞增繫結資料行的位址時，結果會指向下一個資料列中相同資料行的起始處。 在 ANSI C 中使用 `sizeof` 運算子時，可保證此項行為。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|APD|SQLINTEGER*|預設值為 Null 指標。<br /><br /> 如果此欄位非 Null，則驅動程式會取消指標的參考、將取消參考的值加入至描述項記錄中的每個延遲欄位 (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR)，然後使用新的指標值來存取資料值。|  
  
 這些欄位只有在使用資料表值參數時才有效，其他的資料類型會加以忽略。  
  
 SQL_CA_SS_TYPE_NAME 對預存程序呼叫而言是選擇性的。 必須針對不是程序呼叫的 SQL 陳述式指定這個欄位，才能讓伺服器判斷資料表值參數的類型。  
  
 如果需要類型名稱，且資料表值參數的資料表類型是定義於預存程序以外的結構描述中，則必須在實作參數描述項 (IPD) 中指定 SQL_CA_SS_TYPE_SCHEMA_NAME。 如果沒有指定，伺服器將無法判斷資料表值參數的類型。 當您呼叫 SQLExecute 或 SQLExecDirect 時，這會導致錯誤。 錯誤將具有 SQLSTATE= 07006 和訊息「限制的資料類型屬性違規」。  
  
 資料表值參數資料行可以使用資料列繫結或資料行繫結。 預設為資料行繫結。 資料列繫結可以藉由設定 SQL_ATTR_PARAM_BIND_TYPE 和 SQL_ATTR_ PARAM_BIND_OFFSET_PTR 來指定。 這與資料行和參數的資料列繫結類似。  
  
 SQL_CA_SS_TYPE_CATALOG_NAME 和 SQL_CA_SS_TYPE_SCHEMA_NAME 也可以用來擷取與 CLR 使用者定義型別參數相關聯的目錄和結構描述。 這些欄位是這些類型現有之類型特定目錄結構描述屬性的替代項目。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的資料表值參數](table-valued-parameters-odbc.md)  
  
  
