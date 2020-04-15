---
title: SSVARIANT 結構 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cd20624744c9870cf5688c22af751d29d990a2db
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296961"
---
# <a name="ssvariant-structure"></a>SSVARIANT 結構
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SSVARIANT**結構在 sqlncli.h 中定義,對應於本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLEDB 提供程式中DBTYPE_SQLVARIANT值。  
  
 **SSVARIANT** 是一個區分集合聯集。 根據 vt 成員的值而定，取用者可以判斷要讀取的成員。 vt 值會對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 因此，**SSVARIANT** 結構可以保留任何 SQL Server 類型。 如需適用於標準 OLE DB 類型之資料結構的詳細資訊，請參閱[類型指示器](https://go.microsoft.com/fwlink/?LinkId=122171) \(英文\)。  
  
## <a name="remarks"></a>備註  
 當 DataTypeCompat==80 時，數個 **SSVARIANT** 子類型會變成字串。 例如，下列 vt 值在 **SSVARIANT** 中會顯示為 VT_SS_WVARSTRING：  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 當 DateTypeCompat == 0 時，這些類型都會以原生形式出現。  
  
 有關SSPROP_INIT_DATATYPECOMPATIBILITY的詳細資訊,請參閱[使用與 SQL Server 本機客戶端的連接字串關鍵字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 sqlncli.h 檔包含變體存取巨集,可簡化**SSVARIANT**結構中成員類型的取消引用。 V_SS_DATETIMEOFFSET 即為一例，可以按照下列方式使用：  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 有關**SSVARIANT**結構每個成員的完整訪問宏集,請參閱 sqlncli.hi 檔。  
  
 下表將描述 **SSVARIANT** 結構的成員：  
  
|member|OLE DB 類型指標|OLE DB C 資料類型|vt 值|註解|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||指定包含在 **SSVARIANT** 結構中的值類型。|  
|bTinyIntVal|DBTYPE_UI1|**位元組**|**VT_SS_UI1**|支援**小字體**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。|  
|sShortIntVal|DBTYPE_I2|**短**|**VT_SS_I2**|支援**小字體**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。|  
|lIntVal|DBTYPE_I4|**長**|**VT_SS_I4**|支援**int**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型。|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|支援**大因資料型態**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|fltRealVal|DBTYPE_R4|**浮動**|**VT_SS_R4**|支持**實際**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|支援**浮點**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|支援 **money** 和 **smallmoney**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|支援**位**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。|  
|rgbGuidVal|DBTYPE_GUID|**Guid**|**VT_SS_GUID**|支援**唯一標識符**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|支援**數位**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|支援**日期**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|支援 **smalldatetime**、**datetime** 和 **datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|支持**時間**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。<br /><br /> 包括下列成員：<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**BYTE**) 指定 *tTime2Val* 值的範圍。|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|支援**日期時間2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。<br /><br /> 包括下列成員：<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**BYTE**) 指定 *tsDataTimeVal* 值的範圍。|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|支援**日期時間偏移**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型。<br /><br /> 包括下列成員：<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**BYTE**) 指定 *tsoDateTimeOffsetVal* 值的範圍。|  
|NCharVal|沒有對應的 OLE DB 類型指標。|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|支援 **nchar** 和 **nvarchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> 包括下列成員：<br /><br /> *sActualLength* (**SHORT**) 指定 *pwchNCharVal* 指向之字串的實際長度。 不包括結尾的零。<br /><br /> *sMaxLength* (**SHORT**) 指定 *pwchNCharVal* 指向之字串的最大長度。<br /><br /> *pwchNCharVal* (**WCHAR** \*) 指向字串的指標。<br /><br /> 未使用的成員：*rgbReserved*、*dwReserved* 及 *pwchReserved*。|  
|CharVal|沒有對應的 OLE DB 類型指標。|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|支援 **char** 和 **varchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> 包括下列成員：<br /><br /> *sActualLength* (**SHORT**) 指定 *pchCharVal* 指向之字串的實際長度。 不包括結尾的零。<br /><br /> *sMaxLength* (**SHORT**) 指定 *pchCharVal* 指向之字串的最大長度。<br /><br /> *pchCharVal* (**CHAR** \*) 指向字串的指標。<br /><br /> 未使用的成員：<br /><br /> *rgbReserved*、*dwReserved* 及 *pwchReserved*。|  
|BinaryVal|沒有對應的 OLE DB 類型指標。|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|支援 **binary** 和 **varbinary**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> 包括下列成員：<br /><br /> *sActualLength* (**SHORT**) 指定 *prgbBinaryVal* 指向之資料的實際長度。<br /><br /> *sMaxLength* (**SHORT**) 指定 *prgbBinaryVal* 指向之資料的最大長度。<br /><br /> *prgbBinaryVal* (**BYTE** \*) 指向二進位資料的指標。<br /><br /> 未使用的成員：*dwReserved*。|  
|UnknownType|未使用|未使用|未使用|未使用|  
|BLOBType|未使用|未使用|未使用|未使用|  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
