---
title: bcp_getcolfmt |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_getcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e9b87bcfd88b4401ad79d3a3a6afe174df94a29d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761146"
---
# <a name="bcpgetcolfmt"></a>bcp_getcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  用來尋找資料行格式屬性值。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_getcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbvalue,  
        INT* pcbLen);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *field*  
 這是擷取屬性的資料行編號。  
  
 *property*  
 這是其中一個屬性常數。  
  
 *pValue*  
 這是要擷取屬性值之緩衝區的指標。  
  
 *cbValue*  
 這是屬性緩衝區的長度 (以位元組為單位)。  
  
 *pcbLen*  
 屬性緩衝區中傳回之資料長度的指標。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 資料行格式屬性值會列在[bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)主題。 資料行格式屬性值為藉由呼叫**bcp_setcolfmt**函式，而**bcp_getcolfmt**函式用來尋找資料行格式屬性值。  
  
 當連接到的行為變更可能會觀察到[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]（或更新版本） 伺服器電腦上，相較於先前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。 如需詳細資訊，請參閱 <<c0> [ 中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt 對於增強型日期和時間功能的支援  
 搭配使用的型別**BCP_FMT_TYPE**日期/時間類型的屬性中所指定[增強型日期和時間類型的大量複製變更&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 日期和時間改善&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
