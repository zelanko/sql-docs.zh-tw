---
title: "DataTypeEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 289d11f586fc1bd583baeb615ce3cff491949ccc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="datatypeenum"></a>DataTypeEnum
指定的資料型別[欄位](../../../ado/reference/ado-api/field-object.md)，[參數](../../../ado/reference/ado-api/parameter-object.md)，或[屬性](../../../ado/reference/ado-api/property-object-ado.md)。 下表描述資料行中的括號會顯示對應的 OLE DB 類型指標。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|旗標值一律會結合其他的資料類型常數，表示其他資料類型的陣列。 不適用於 ADOX。|  
|**adBigInt**|20|指出八位元組帶正負號的整數 (DBTYPE_I8)。|  
|**adBinary**|128|表示二進位值 (DBTYPE_BYTES)。|  
|**adBoolean**|11|指出**布林**值 (DBTYPE_BOOL)。|  
|**adBSTR**|8|表示 null 結束的字元字串 (Unicode) (DBTYPE_BSTR)。|  
|**adChapter**|136|表示可識別子資料列集 (DBTYPE_HCHAPTER) 中的資料列的第四個位元組值。|  
|**adChar**|129|表示字串值 (DBTYPE_STR)。|  
|**adCurrency**|6|表示貨幣值 (DBTYPE_CY)。 貨幣是小數點右邊的四位數的定點數字。 它會儲存在 10,000 調整的八位元組帶正負號整數。|  
|**adDate**|7|表示 date 值 (DBTYPE_DATE)。 日期會儲存為 double，值的整數部分為自 1899 年 12 月 30 日的天數，而其中小數部分是一天的分數。|  
|**adDBDate**|133|表示日期 (yyyymmdd) (DBTYPE_DBDATE)。|  
|**adDBTime**|134|表示時間值 (hhmmss) (DBTYPE_DBTIME)。|  
|**adDBTimeStamp**|135|表示日期/時間戳記 （yyyymmddhhmmss 加上在十億分之一分數） (DBTYPE_DBTIMESTAMP)。|  
|**adDecimal**|14|指出固定有效位數和小數位數 (DBTYPE_DECIMAL) 的精確數值。|  
|**adDouble**|5|表示雙精度浮點數值 (DBTYPE_R8)。|  
|**adEmpty**|0|不指定任何值 (DBTYPE_EMPTY)。|  
|**adError**|10|表示 32 位元錯誤碼 (DBTYPE_ERROR)。|  
|**adFileTime**|64|表示 64 位元值的 100 奈秒間隔數表示自 1601 年 1 月 1 日 (DBTYPE_FILETIME)。|  
|**adGUID**|72|表示全域唯一識別碼 (GUID) (DBTYPE_GUID)。|  
|**adIDispatch**|9|指出指標**IDispatch** COM 物件 (DBTYPE_IDISPATCH) 上的介面。<br /><br /> **請注意**由 ADO 目前不支援這種資料類型。 使用方式可能會造成無法預期的結果。|  
|**adInteger**|3|指出四位元組帶正負號的整數 (DBTYPE_I4)。|  
|**adIUnknown**|13|指出指標**IUnknown** COM 物件 (DBTYPE_IUNKNOWN) 上的介面。<br /><br /> **請注意**由 ADO 目前不支援這種資料類型。 使用方式可能會造成無法預期的結果。|  
|**adLongVarBinary**|205|表示較長的二進位值。|  
|**adLongVarChar**|201|表示較長的字串值。|  
|**adLongVarWChar**|203|表示長時間的 null 結束的 Unicode 字串值。|  
|**adNumeric**|131|指出固定有效位數和小數位數 (DBTYPE_NUMERIC) 的精確數值。|  
|**adPropVariant**|138|指出自動化 PROPVARIANT (DBTYPE_PROP_VARIANT)。|  
|**adSingle**|4|表示單精確度浮點數值 (DBTYPE_R4)。|  
|**adSmallInt**|2|指出兩個位元組帶正負號的整數 (DBTYPE_I2)。|  
|**adTinyInt**|16|表示單位元組帶正負號的整數 (DBTYPE_I1)。|  
|**adUnsignedBigInt**|21|表示八位元組不帶正負號的整數 (DBTYPE_UI8)。|  
|**adUnsignedInt**|19|表示四位元組不帶正負號的整數 (DBTYPE_UI4)。|  
|**adUnsignedSmallInt**|18|表示兩個位元組不帶正負號的整數 (DBTYPE_UI2)。|  
|**adUnsignedTinyInt**|17|表示單位元組不帶正負號的整數 (DBTYPE_UI1)。|  
|**adUserDefined**|132|表示使用者定義的變數 (DBTYPE_UDT)。|  
|**adVarBinary**|204|表示二進位值。|  
|**adVarChar**|200|表示字串值。|  
|**adVariant**|12|指出自動化**Variant** (DBTYPE_VARIANT)。<br /><br /> **請注意**由 ADO 目前不支援這種資料類型。 使用方式可能會造成無法預期的結果。|  
|**adVarNumeric**|139|表示數字的值。|  
|**adVarWChar**|202|表示以 null 結束的 Unicode 字元字串。|  
|**adWChar**|130|表示 null 結束的 Unicode 字元字串 (DBTYPE_WSTR)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.DataType.ARRAY|  
|AdoEnums.DataType.BIGINT|  
|AdoEnums.DataType.BINARY|  
|AdoEnums.DataType.BOOLEAN|  
|AdoEnums.DataType.BSTR|  
|AdoEnums.DataType.CHAPTER|  
|AdoEnums.DataType.CHAR|  
|AdoEnums.DataType.CURRENCY|  
|AdoEnums.DataType.DATE|  
|AdoEnums.DataType.DBDATE|  
|AdoEnums.DataType.DBTIME|  
|AdoEnums.DataType.DBTIMESTAMP|  
|AdoEnums.DataType.DECIMAL|  
|AdoEnums.DataType.DOUBLE|  
|AdoEnums.DataType.EMPTY|  
|AdoEnums.DataType.ERROR|  
|AdoEnums.DataType.FILETIME|  
|AdoEnums.DataType.GUID|  
|AdoEnums.DataType.IDISPATCH|  
|AdoEnums.DataType.INTEGER|  
|AdoEnums.DataType.IUNKNOWN|  
|AdoEnums.DataType.LONGVARBINARY|  
|AdoEnums.DataType.LONGVARCHAR|  
|AdoEnums.DataType.LONGVARWCHAR|  
|AdoEnums.DataType.NUMERIC|  
|AdoEnums.DataType.PROPVARIANT|  
|AdoEnums.DataType.SINGLE|  
|AdoEnums.DataType.SMALLINT|  
|AdoEnums.DataType.TINYINT|  
|AdoEnums.DataType.UNSIGNEDBIGINT|  
|AdoEnums.DataType.UNSIGNEDINT|  
|AdoEnums.DataType.UNSIGNEDSMALLINT|  
|AdoEnums.DataType.UNSIGNEDTINYINT|  
|AdoEnums.DataType.USERDEFINED|  
|AdoEnums.DataType.VARBINARY|  
|AdoEnums.DataType.VARCHAR|  
|AdoEnums.DataType.VARIANT|  
|AdoEnums.DataType.VARNUMERIC|  
|AdoEnums.DataType.VARWCHAR|  
|AdoEnums.DataType.WCHAR|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|  
|[CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|[型別屬性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)|

