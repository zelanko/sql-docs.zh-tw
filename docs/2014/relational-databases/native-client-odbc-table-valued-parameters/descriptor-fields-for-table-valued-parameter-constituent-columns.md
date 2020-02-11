---
title: 資料表值參數組成資料行的描述項欄位 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a31491b56e5b5cd700e744be2b7a84f10f1e0121
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63199933"
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>資料表值參數組成資料行的描述項欄位
  本節中所述的資料表值參數描述項欄位是使用[SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md)和[SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md)搭配執行參數描述元（IPD）的控制碼來進行操作。  
  
## <a name="remarks"></a>備註  
 SQL_DESC_AUTO_UNIQUE_VALUE 用於資料表值參數與其他功能。  
  
|屬性名稱|類型|描述|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE 表示此資料行是識別資料行。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以使用此資訊來優化效能，但不需要應用程式來設定識別欄位。|  
  
 下列屬性會加入到應用程式參數描述項 (APD) 和實作參數描述項 (IPD) 的所有參數類型中：  
  
|屬性名稱|類型|描述|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE 表示此資料行是計算資料行。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以使用這種資訊來優化效能，但是應用程式不需要針對計算資料行設定它。<br /><br /> 若是非資料表值參數資料行的繫結，會忽略此屬性。|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE 表示資料表值參數資料行參與唯一的索引鍵。 這會使查詢效能更好。 若是非資料表值參數資料行的繫結，會忽略此屬性。|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|表示資料表值參數資料行的排序次序。 這會使查詢效能更好。 若是非資料表值參數資料行的繫結，會忽略此屬性。 以下是可能的值：<br /><br /> -SQL_SS_ASCENDING_ORDER<br />-SQL_SS_DESCENDING_ORDER<br />-SQL_SS_ORDER_UNSPECIFIED<br /><br /> SQL_SS_ASCENDING_ORDER 和 SQL_SS_DESCENDING_ORDER 以外的值會產生 SQLSTATE HY024 的錯誤，並出現訊息「屬性值無效」，而且這些值會視為 SQL_SS_ORDER_UNSPECIFIED，也就是此屬性的預設值。|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|表示在定義資料表值參數之整體順序的一組資料行中，資料表值參數資料行的序數。 這會使查詢效能更好。 若是非資料表值參數資料行的繫結，會忽略此屬性。 排序序數會從 1 開始。 預設值 0 表示資料表值參數資料行沒有資料行順序。|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|表示資料表值參數中的所有資料列對於此資料行是否有預設值。 對於資料表值參數，無法逐資料列選取預設值。 SQL_FALSE 的值表示這些資料列將沒有預設值。 這是預設值。 SQL_TRUE 的值表示此資料行對於所有資料列都有預設值。<br /><br /> 如果設定為 SQL_TRUE，則不會將任何資料傳送到伺服器。<br /><br /> 如果伺服器處理不需要資料行值，此欄位也可以搭配識別或計算資料行使用。|  
  
 這些屬性只適用於資料表值參數資料行。 若是其他參數，則會忽略這些屬性。  
  
 如果針對資料表值參數資料行設定 SQL_CA_SS_COL_HAS_DEFAULT_VALUE，該資料行的 SQL_DESC_DATA_PTR 必須為 Null 指標。 否則，SQLExecute 或 SQLExecDirect 會傳回 SQL_ERROR。 將會\<產生含有 SQLSTATE = 07S01 的診斷記錄，以及「參數 p>，資料行\<c>」的預設參數用法無效，其中\<p> 是參數序數，而\<c> 是資料行序數。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的資料表值參數](table-valued-parameters-odbc.md)  
  
  
