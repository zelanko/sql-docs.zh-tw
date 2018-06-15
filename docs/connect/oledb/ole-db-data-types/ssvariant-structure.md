---
title: SSVARIANT 結構 |Microsoft 文件
description: OLE DB 驅動程式中的 SQL Server 的 SSVARIANT 結構
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 9afd7d6ce87ac49c060347287d4b7a081ea5bb41
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2018
ms.locfileid: "35666378"
---
# <a name="ssvariant-structure"></a>SSVARIANT 結構
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **SSVARIANT**結構，定義在 msoledbsql.h，對應至 OLE DB 驅動程式中的 DBTYPE_SQLVARIANT 值的 SQL Server。  
  
 **SSVARIANT**是辨識聯集。 根據 vt 成員的值，取用者可以判斷要讀取的成員。 vt 值會對應至[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。 因此， **SSVARIANT**結構可以保存任何 SQL Server 類型。 如需有關標準 OLE DB 類型的資料結構的詳細資訊，請參閱[類型指標](http://go.microsoft.com/fwlink/?LinkId=122171)。  
  
## <a name="remarks"></a>備註  
 當 DataTypeCompat = = 80 時，數個**SSVARIANT**子類型會變成字串。 例如，下列 vt 值將會出現在**SSVARIANT**為 VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 當 DateTypeCompat == 0 時，這些類型都會以原生形式出現。  
  
 如需有關 SSPROP_INIT_DATATYPECOMPATIBILITY 的詳細資訊，請參閱[搭配 OLE DB 驅動程式的 SQL Server 中使用連接字串關鍵字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  
  
 Msoledbsql.h 檔案包含簡化取值中的成員類型的變數存取巨集**SSVARIANT**結構。 V_SS_DATETIMEOFFSET 即為一例，可以按照下列方式使用：  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 如需完整存取巨集的每個成員**SSVARIANT**結構時，請參閱 msoledbsql.h 檔案。  
  
 下表描述的成員**SSVARIANT**結構：  
  
|成員|OLE DB 類型指標|OLE DB C 資料類型|vt 值|註解|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||指定值中包含的型別**SSVARIANT**結構。|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|支援**tinyint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|sShortIntVal|DBTYPE_I2|**短**|**VT_SS_I2**|支援**smallint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|lIntVal|DBTYPE_I4|**長**|**VT_SS_I4**|支援**int** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|支援**bigint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|支援**真實**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|支援**float** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|支援**money**和**smallmoney** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|支援**元**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|支援**uniqueidentifier** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|支援**數值**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|支援**日期**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|支援**smalldatetime**， **datetime**，和**datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|支援**時間**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。<br /><br /> 包括下列成員：<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**位元組**) 指定的小數位數*tTime2Val*值。|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|支援**datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。<br /><br /> 包括下列成員：<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**位元組**) 指定的小數位數*tsDataTimeVal*值。|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|支援**datetimeoffset** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。<br /><br /> 包括下列成員：<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**位元組**) 指定的小數位數*tsoDateTimeOffsetVal*值。|  
|NCharVal|沒有對應的 OLE DB 類型指標。|**結構 _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|支援**nchar**和**nvarchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。<br /><br /> 包括下列成員：<br /><br /> *sActualLength* (**簡短**) 指定之字串的實際長度*pwchNCharVal*點。 不包括結尾的零。<br /><br /> *sMaxLength* (**簡短**) 指定之字串的最大長度*pwchNCharVal*點。<br /><br /> *pwchNCharVal* (**WCHAR** \*) 字串的指標。<br /><br /> 未使用的成員： *rgbReserved*， *dwReserved*，和*pwchReserved*。|  
|CharVal|沒有對應的 OLE DB 類型指標。|**結構 _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|支援**char**和**varchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。<br /><br /> 包括下列成員：<br /><br /> *sActualLength* (**簡短**) 指定之字串的實際長度*pchCharVal*點。 不包括結尾的零。<br /><br /> *sMaxLength* (**簡短**) 指定之字串的最大長度*pchCharVal*點。<br /><br /> *pchCharVal* (**CHAR** \*) 字串的指標。<br /><br /> 未使用的成員：<br /><br /> *rgbReserved*， *dwReserved*，和*pwchReserved*。|  
|BinaryVal|沒有對應的 OLE DB 類型指標。|**結構 _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|支援**二進位**和**varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。<br /><br /> 包括下列成員：<br /><br /> *sActualLength* (**簡短**) 指定之資料的實際長度*prgbBinaryVal*點。<br /><br /> *sMaxLength* (**簡短**) 指定之資料的最大長度*prgbBinaryVal*點。<br /><br /> *prgbBinaryVal* (**位元組** \*) 的二進位資料的指標。<br /><br /> 未使用的成員： *dwReserved*。|  
|UnknownType|未使用|未使用|未使用|未使用|  
|BLOBType|未使用|未使用|未使用|未使用|  
  
## <a name="see-also"></a>另請參閱  
 [資料型別&#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
