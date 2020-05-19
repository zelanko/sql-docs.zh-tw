---
title: bcp_getcolfmt |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_getcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 793543cce582bd4e17cbf8d06f096056a2ecb89b
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82701969"
---
# <a name="bcp_getcolfmt"></a>bcp_getcolfmt
  用來尋找資料行格式屬性值。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_getcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbvalue,  
INT*   
pcbLen  
);  
  
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
 資料行格式屬性值列在[bcp_setcolfmt](bcp-setcolfmt.md)主題中。 資料行格式屬性值是藉由呼叫**bcp_setcolfmt**函數來設定，而**bcp_getcolfmt**函數則是用來尋找資料行格式屬性值。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]相較于舊版，連接到（或更新版本）伺服器電腦時，可能會觀察到行為變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[中繼資料探索](../native-client/features/metadata-discovery.md)。  
  
## <a name="bcp_getcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt 對於增強型日期和時間功能的支援  
 與日期/時間類型的屬性搭配使用的類型， `BCP_FMT_TYPE` 會如[針對增強型日期和時間類型的大量複製變更中所指定 &#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
