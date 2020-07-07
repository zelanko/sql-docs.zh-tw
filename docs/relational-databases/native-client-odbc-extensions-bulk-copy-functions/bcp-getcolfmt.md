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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e279af67313107d495e5ef864414e53997c3cff
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010117"
---
# <a name="bcp_getcolfmt"></a>bcp_getcolfmt
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

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
  
 *欄位*  
 這是擷取屬性的資料行編號。  
  
 *property*  
 這是其中一個屬性常數。  
  
 *pValue*  
 這是要擷取屬性值之緩衝區的指標。  
  
 *cbValue*  
 這是屬性緩衝區的長度 (以位元組為單位)。  
  
 *pcbLen*  
 屬性緩衝區中傳回之資料長度的指標。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 資料行格式屬性值列在[bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)主題中。 資料行格式屬性值是藉由呼叫**bcp_setcolfmt**函數來設定，而**bcp_getcolfmt**函數則是用來尋找資料行格式屬性值。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]相較于舊版，連接到（或更新版本）伺服器電腦時，可能會觀察到行為變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="bcp_getcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt 對於增強型日期和時間功能的支援  
 與日期/時間類型的**BCP_FMT_TYPE**屬性搭配使用的類型，會如[針對增強型日期和時間類型的大量複製變更（&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)中所指定）。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
