---
title: bcp_gettypename |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_gettypename
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5bc7caa063d14967e576fd009a23110b9647836b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62689022"
---
# <a name="bcp_gettypename"></a>bcp_gettypename
  傳回指定之 BCP 類型 Token 的 SQL 類型名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_gettypename (  
INT   
token  
,  
DBBOOL   
fIsMaxType  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *權杖*  
 指出 BCP 類型 Token 的值。  
  
 *欄位*  
 指出要求的 Token 是否為最大值類型。  
  
## <a name="returns"></a>傳回值  
 包含對應到 BCP 類型之 SQL 類型名稱的字串。 如果指定無效的 BCP 類型，則傳回空字串。  
  
## <a name="remarks"></a>備註  
 BCP 類型 Token 是在 sqlncli.h 標頭檔和 sqlncli11.lib 程式庫中定義的。  
  
 以下的資料表會指定可能的 BCP 類型 (不論它們是否為最大類型) 以及預期的輸出。  
  
|BCP 類型名稱|MaxType|輸出|  
|-------------------|-------------|------------|  
|`SQLDECIMAL`|無論是|**decimal**|  
|`SQLNUMERIC`|無論是|**數值**|  
|`SQLINT1`|無論是|**tinyint**|  
|`SQLINT2`|無論是|**smallint**|  
|`SQLINT4`|無論是|**int**|  
|`SQLMONEY`|無論是|**money**|  
|`SQLFLT8`|無論是|**float**|  
|`SQLDATETIME`|無論是|**datetime**|  
|`SQLBITN`|無論是|**bit-null**|  
|`SQLBIT`|無論是|**bit**|  
|`SQLBIGCHAR`|否|**char**|  
|`SQLCHARACTER`|否|**char**|  
|`SQLBIGVARCHAR`|否|**varchar**|  
|`SQLVARCHAR`|否|**varchar**|  
|`SQLTEXT`|無論是|**text**|  
|`SQLBIGBINARY`|否|**binary**|  
|`SQLBINARY`|否|**二**|  
|`SQLBIGVARBINARY`|否|**Varbinary**|  
|`SQLVARBINARY`|否|**Varbinary**|  
|`SQLIMAGE`|無論是|**包**|  
|`SQLINTN`|無論是|**int-null**|  
|`SQLDATETIMN`|無論是|**datetime-null**|  
|`SQLMONEYN`|無論是|**money-null**|  
|`SQLFLTN`|無論是|**float-null**|  
|`SQLAOPSUM`|無論是|**要求**|  
|`SQLAOPAVG`|無論是|**Avg**|  
|`SQLAOPCNT`|無論是|**計數**|  
|`SQLAOPMIN`|無論是|**分鐘**|  
|`SQLAOPMAX`|無論是|**讀數**|  
|`SQLDATETIM4`|無論是|**smalldatetime**|  
|`SQLMONEY4`|無論是|**Smallmoney**|  
|`SQLFLT4`|無論是|**Real**|  
|`SQLUNIQUEID`|無論是|**uniqueidentifier**|  
|`SQLNCHAR`|否|**Nchar**|  
|`SQLNVARCHAR`|否|**NVarchar**|  
|`SQLNTEXT`|無論是|**Ntext**|  
|`SQLVARIANT`|無論是|**sql_variant**|  
|`SQLINT8`|無論是|**Bigint**|  
|`SQLCHARACTER`|是|**varchar(max)**|  
|`SQLBIGCHAR`|是|**varchar(max)**|  
|`SQLBIGVARCHAR`|是|**varchar(max)**|  
|`SQLVARCHAR`|是|**varchar(max)**|  
|`SQLBINARY`|是|**varbinary(max)**|  
|`SQLBIGBINARY`|是|**varbinary(max)**|  
|`SQLBIGVARBINARY`|是|**varbinary(max)**|  
|`SQLVARBINARY`|是|**varbinary(max)**|  
|`SQLNCHAR`|是|**nvarchar(max)**|  
|`SQLNVARCHAR`|是|**nvarchar(max)**|  
|`SQLXML`|是|**Stl**|  
|`SQLUDT`|無論是|**Udt**|  
  
## <a name="bcp_gettypename-support-for-enhanced-date-and-time-features"></a>bcp_gettypename 支援增強的日期和時間功能  
 適用于日期/時間類型的 token 參數值會在[&#40;OLE DB 和 ODBC&#41;的增強型日期和時間類型的大量複製變更](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)中，描述于資料表中的 "Type in sqlncli. h" 資料行。 傳回值位於 "File storage type" 資料行的對應資料列中。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
