---
description: DataTypeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ec805f403e3f76cacde3374cda091bf9b587b74c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444200"
---
# <a name="datatypeenum"></a>DataTypeEnum
指定 [欄位](../../../ado/reference/ado-api/field-object.md)、 [參數](../../../ado/reference/ado-api/parameter-object.md)或 [屬性](../../../ado/reference/ado-api/property-object-ado.md)的資料類型。 對應的 OLE DB 類型指標會顯示在下表的 [描述] 資料行中的括弧內。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|旗標值，一律與另一個資料類型常數結合，表示其他資料類型的陣列。 不適用 ADOX。|  
|**adBigInt**|20|指出 (DBTYPE_I8) 的八位元組帶正負號的整數。|  
|**adBinary**|128|指出 (DBTYPE_BYTES) 的二進位值。|  
|**adBoolean**|11|指出 (DBTYPE_BOOL) 的 **布林** 值。|  
|**adBSTR**|8|表示以 null 結束的字元字串 (Unicode)  (DBTYPE_BSTR) 。|  
|**adChapter**|136|指出四個位元組的章節值，識別子資料列集中的資料列 (DBTYPE_HCHAPTER) 。|  
|**adChar**|129|指出 (DBTYPE_STR) 的字串值。|  
|**adCurrency**|6|指出貨幣值 (DBTYPE_CY) 。 Currency 是小數點右邊有四位數的固定點數位。 它會以8位元組帶正負號的整數儲存，並以10000來調整。|  
|**adDate**|7|表示日期值 (DBTYPE_DATE) 。 日期會儲存為雙精度浮點數，其中的整個部分是自1899年12月30日起的天數，而分數部分則為一天的分數。|  
|**adDBDate**|133|指出 (yyyymmdd)  (DBTYPE_DBDATE) 的日期值。|  
|**adDBTime**|134|指出時間值 (hhmmss)  (DBTYPE_DBTIME) 。|  
|**adDBTimeStamp**|135|表示日期/時間戳記 (yyyymmddhhmmss.ffffff 加上 billionths)  (DBTYPE_DBTIMESTAMP) 中的分數。|  
|**adDecimal**|14|指出具有固定有效位數和小數位數 (DBTYPE_DECIMAL) 的精確數值。|  
|**adDouble**|5|指出 (DBTYPE_R8) 的雙精確度浮點值。|  
|**adEmpty**|0|指定 (DBTYPE_EMPTY) 的值。|  
|**adError**|10|指出 (DBTYPE_ERROR) 的32位錯誤碼。|  
|**adFileTime**|64|表示64位值，表示自年1月 1 1601 日起， (DBTYPE_FILETIME) 的 100-秒間隔數。|  
|**adGUID**|72|指出 (GUID)  (DBTYPE_GUID) 的全域唯一識別碼。|  
|**adIDispatch**|9|表示 COM 物件上的 **IDispatch** 介面指標， (DBTYPE_IDISPATCH) 。<br /><br /> **注意** ADO 目前不支援此資料類型。 使用方式可能會導致無法預期的結果。|  
|**adInteger**|3|指出 (DBTYPE_I4) 的四位元組帶正負號的整數。|  
|**adIUnknown**|13|表示 COM 物件上的 **IUnknown** 介面指標， (DBTYPE_IUNKNOWN) 。<br /><br /> **注意** ADO 目前不支援此資料類型。 使用方式可能會導致無法預期的結果。|  
|**adLongVarBinary**|205|表示長的二進位值。|  
|**adLongVarChar**|201|表示長字串值。|  
|**adLongVarWChar**|203|表示長的以 null 結束的 Unicode 字串值。|  
|**adNumeric**|131|指出具有固定有效位數和小數位數 (DBTYPE_NUMERIC) 的精確數值。|  
|**adPropVariant**|138|表示自動化 PROPVARIANT (DBTYPE_PROP_VARIANT) 。|  
|**adSingle**|4|指出 (DBTYPE_R4) 的單精確度浮點值。|  
|**adSmallInt**|2|指出 (DBTYPE_I2) 的雙位元組帶正負號的整數。|  
|**adTinyInt**|16|指出 (DBTYPE_I1) 的一個位元組帶正負號的整數。|  
|**adUnsignedBigInt**|21|指出 (DBTYPE_UI8) 的八位元組不帶正負號的整數。|  
|**adUnsignedInt**|19|指出 (DBTYPE_UI4) 的四位元組不帶正負號的整數。|  
|**adUnsignedSmallInt**|18|指出 (DBTYPE_UI2) 的雙位元組不帶正負號的整數。|  
|**adUnsignedTinyInt**|17|指出 (DBTYPE_UI1) 的單位元組不帶正負號的整數。|  
|**adUserDefined**|132|指出 (DBTYPE_UDT) 的使用者自訂變數。|  
|**adVarBinary**|204|表示二進位值。|  
|**adVarChar**|200|表示字串值。|  
|**adVariant**|12|指出 (DBTYPE_VARIANT) 的自動化 **變異** 。<br /><br /> **注意** ADO 目前不支援此資料類型。 使用方式可能會導致無法預期的結果。|  
|**adVarNumeric**|139|表示數位值。|  
|**adVarWChar**|202|表示以 null 終止的 Unicode 字元字串。|  
|**adWChar**|130|指出 (DBTYPE_WSTR) 之以 null 結束的 Unicode 字元字串。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums|  
|AdoEnums，資料類型 BIGINT|  
|AdoEnums 資料類型二進位|  
|AdoEnums。布林值|  
|AdoEnums|  
|AdoEnums 的資料類型章節|  
|AdoEnums|  
|AdoEnums 貨幣|  
|AdoEnums，日期類型|  
|AdoEnums。 DBDATE|  
|AdoEnums。 DBTIME|  
|AdoEnums。 DBTIMESTAMP|  
|AdoEnums： DECIMAL|  
|AdoEnums。 DOUBLE|  
|AdoEnums，資料類型空白|  
|AdoEnums。錯誤|  
|AdoEnums，資料類型 FILETIME|  
|AdoEnums 的資料類型 GUID|  
|AdoEnums，資料類型. IDISPATCH|  
|AdoEnums，整數|  
|AdoEnums 資料類型. IUNKNOWN|  
|AdoEnums。 LONGVARBINARY|  
|AdoEnums。 LONGVARCHAR|  
|AdoEnums。 LONGVARWCHAR|  
|AdoEnums，NUMERIC|  
|AdoEnums。 PROPVARIANT|  
|AdoEnums 單一資料類型|  
|AdoEnums，資料類型. SMALLINT|  
|AdoEnums，資料類型 TINYINT|  
|AdoEnums。 UNSIGNEDBIGINT|  
|AdoEnums。 UNSIGNEDINT|  
|AdoEnums。 UNSIGNEDSMALLINT|  
|AdoEnums。 UNSIGNEDTINYINT|  
|AdoEnums：使用者類型|  
|AdoEnums，資料類型|  
|AdoEnums，資料類型 VARCHAR|  
|AdoEnums。 VARIANT|  
|AdoEnums。 VARNUMERIC|  
|AdoEnums。 VARWCHAR|  
|AdoEnums。 WCHAR|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
        [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)  
        [Type 屬性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)  
    :::column-end:::
:::row-end:::
