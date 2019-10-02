---
title: bcp_getcolfmt | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 40e7f63438bbe6ff68284aa573e1307b17087234
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707539"
---
# <a name="bcp_getcolfmt"></a>bcp_getcolfmt
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
 資料行格式屬性值會列在[bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)主題中。 資料行格式屬性值是藉由呼叫**bcp_setcolfmt**函數來設定，而**bcp_getcolfmt**函數則是用來尋找資料行格式屬性值。  
  
 相較于舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版，連接到 @no__t 0 （或更新版本）伺服器電腦時，可能會發現行為變更。 如需詳細資訊, 請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="bcp_getcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt 對於增強型日期和時間功能的支援  
 與日期/時間類型的**BCP_FMT_TYPE**屬性搭配使用的類型，會如[針對增強型日期和時間類型&#40;OLE DB 和 ODBC&#41;的大量複製變更](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)中所指定。  
  
 如需詳細資訊，請參閱[日期和&#40;時間&#41;改善 ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
