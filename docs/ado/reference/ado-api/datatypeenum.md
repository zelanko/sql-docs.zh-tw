---
title: DataTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27386894ce6d1d393505d49b4863a0ba9bf3320b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933228"
---
# <a name="datatypeenum"></a>DataTypeEnum
指定[欄位](../../../ado/reference/ado-api/field-object.md)、[參數](../../../ado/reference/ado-api/parameter-object.md)或[屬性](../../../ado/reference/ado-api/property-object-ado.md)的資料類型。 對應的 OLE DB 類型指標會顯示在下表的 [描述] 資料行中的括弧內。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|旗標值，一律與另一個資料類型常數結合，表示另一個資料類型的陣列。 不適用於 ADOX。|  
|**adBigInt**|20|表示八位元組帶正負號的整數（DBTYPE_I8）。|  
|**adBinary**|128|表示二進位值（DBTYPE_BYTES）。|  
|**adBoolean**|11|表示**布林**值（DBTYPE_BOOL）。|  
|**adBSTR**|8|表示以 null 結束的字元字串（Unicode）（DBTYPE_BSTR）。|  
|**adChapter**|136|表示四個位元組的章節值，用以識別子資料列集（DBTYPE_HCHAPTER）中的資料列。|  
|**adChar**|129|表示字串值（DBTYPE_STR）。|  
|**adCurrency**|6|表示貨幣值（DBTYPE_CY）。 「貨幣」是包含小數點右邊四位數的固定點數。 它是以10000所調整的8位元組帶正負號的整數儲存。|  
|**adDate**|7|表示日期值（DBTYPE_DATE）。 日期會儲存為雙精度浮點數，其中的整個部分是自1899年12月30日起的天數，而的小數部分則是一天的分數。|  
|**adDBDate**|133|表示日期值（yyyymmdd）（DBTYPE_DBDATE）。|  
|**adDBTime**|134|表示時間值（hhmmss）（DBTYPE_DBTIME）。|  
|**adDBTimeStamp**|135|表示日期/時間戳記（yyyymmddhhmmss.ffffff 加上 billionths 中的分數）（DBTYPE_DBTIMESTAMP）。|  
|**adDecimal**|14|表示具有固定有效位數和小數位數（DBTYPE_DECIMAL）的精確數值。|  
|**adDouble**|5|表示雙精確度浮點值（DBTYPE_R8）。|  
|**adEmpty**|0|不指定值（DBTYPE_EMPTY）。|  
|**adError**|10|表示32位錯誤碼（DBTYPE_ERROR）。|  
|**adFileTime**|64|表示64位值，代表自1601年1月1日起的 100-毫微秒間隔數（DBTYPE_FILETIME）。|  
|**adGUID**|72|表示全域唯一識別碼（GUID）（DBTYPE_GUID）。|  
|**adIDispatch**|9|表示 COM 物件（DBTYPE_IDISPATCH）上**IDispatch**介面的指標。<br /><br /> **注意**ADO 目前不支援此資料類型。 使用可能會導致無法預期的結果。|  
|**adInteger**|3|表示四位元組帶正負號的整數（DBTYPE_I4）。|  
|**adIUnknown**|13|表示 COM 物件（DBTYPE_IUNKNOWN）上**IUnknown**介面的指標。<br /><br /> **注意**ADO 目前不支援此資料類型。 使用可能會導致無法預期的結果。|  
|**adLongVarBinary**|205|表示長的二進位值。|  
|**adLongVarChar**|201|表示長字串值。|  
|**adLongVarWChar**|203|表示長的以 null 結束的 Unicode 字串值。|  
|**adNumeric**|131|表示具有固定有效位數和小數位數（DBTYPE_NUMERIC）的精確數值。|  
|**adPropVariant**|138|表示自動化 PROPVARIANT （DBTYPE_PROP_VARIANT）。|  
|**adSingle**|4|表示單精確度浮點值（DBTYPE_R4）。|  
|**adSmallInt**|2|表示兩個位元組帶正負號的整數（DBTYPE_I2）。|  
|**adTinyInt**|16|表示一個位元組帶正負號的整數（DBTYPE_I1）。|  
|**adUnsignedBigInt**|21|表示8位元組不帶正負號的整數（DBTYPE_UI8）。|  
|**adUnsignedInt**|19|表示四個位元組不帶正負號的整數（DBTYPE_UI4）。|  
|**adUnsignedSmallInt**|18|表示兩個位元組不帶正負號的整數（DBTYPE_UI2）。|  
|**adUnsignedTinyInt**|17|表示一個位元組不帶正負號的整數（DBTYPE_UI1）。|  
|**adUserDefined**|132|表示使用者定義的變數（DBTYPE_UDT）。|  
|**adVarBinary**|204|表示二進位值。|  
|**adVarChar**|200|表示字串值。|  
|**adVariant**|12|表示自動化**變異**數（DBTYPE_VARIANT）。<br /><br /> **注意**ADO 目前不支援此資料類型。 使用可能會導致無法預期的結果。|  
|**adVarNumeric**|139|表示數值。|  
|**adVarWChar**|202|表示以 null 結束的 Unicode 字元字串。|  
|**adWChar**|130|表示以 null 結束的 Unicode 字元字串（DBTYPE_WSTR）。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. 資料類型陣列|  
|AdoEnums. 資料類型 BIGINT|  
|AdoEnums。 BINARY|  
|AdoEnums。布林值|  
|AdoEnums. 資料類型 BSTR|  
|AdoEnums。資料類型章節|  
|AdoEnums. 資料類型. CHAR|  
|AdoEnums 貨幣類型|  
|AdoEnums 資料類型。日期|  
|AdoEnums. DataType. DBDATE|  
|AdoEnums. DataType. DBTIME|  
|AdoEnums. DataType. DBTIMESTAMP|  
|AdoEnums。 DECIMAL|  
|AdoEnums。 DOUBLE|  
|AdoEnums。資料類型空白|  
|AdoEnums。錯誤|  
|AdoEnums。資料類型 FILETIME|  
|AdoEnums. DataType. GUID|  
|AdoEnums. 資料類型. IDISPATCH|  
|AdoEnums。資料類型整數|  
|AdoEnums。資料類型 IUNKNOWN|  
|AdoEnums. DataType. LONGVARBINARY|  
|AdoEnums. DataType. LONGVARCHAR|  
|AdoEnums. DataType. LONGVARWCHAR|  
|AdoEnums。數值|  
|AdoEnums. DataType. PROPVARIANT|  
|AdoEnums。單一資料類型|  
|AdoEnums。資料類型 SMALLINT|  
|AdoEnums。資料類型 TINYINT|  
|AdoEnums. DataType. UNSIGNEDBIGINT|  
|AdoEnums. DataType. UNSIGNEDINT|  
|AdoEnums. DataType. UNSIGNEDSMALLINT|  
|AdoEnums. DataType. UNSIGNEDTINYINT|  
|AdoEnums。使用者類型|  
|AdoEnums. 資料類型 VARBINARY|  
|AdoEnums. 資料類型 VARCHAR|  
|AdoEnums。 VARIANT|  
|AdoEnums. DataType. VARNUMERIC|  
|AdoEnums. DataType. VARWCHAR|  
|AdoEnums. DataType. WCHAR|  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|  
|[CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|[Type 屬性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)|
