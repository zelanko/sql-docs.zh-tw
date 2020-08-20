---
description: LocalDBFormatMessage 函數
title: LocalDBFormatMessage 函式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBFormatMessage
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5d3083d789124023985577d1a04a811ff2273915
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475837"
---
# <a name="localdbformatmessage-function"></a>LocalDBFormatMessage 函數
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  傳回指定之 SQL Server Express LocalDB 錯誤的當地語系化文字描述。  
  
 **標頭檔：** sqlncli。h  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT LocalDBFormatMessage(  
           HRESULT hrLocalDB,  
           DWORD dwFlags,   
           DWORD dwLanguageId,   
           LPWSTR wszMessage,   
           LPDWORD lpcchMessage   
);  
```  
  
## <a name="parameters"></a>參數  
 *hrLocalDB*  
 [輸入] LocalDB 錯誤碼。  
  
 *dwFlags*  
 [輸入] 指定此函數行為的旗標。  
  
 可用的旗標：  
  
 LOCALDB_TRUNCATE_ERR_MESSAGE  
 如果輸入緩衝區太短，則會截斷錯誤訊息以符合緩衝區。  
  
 *dwLanguageId*  
 [輸入] 所需語言 (LANGID) 或 0，在任何情況下都會使用 Win32 FormatMessage 語言順序。  
  
 *wszMessage*  
 [輸出] 儲存 LocalDB 錯誤訊息的緩衝區。  
  
 *lpcchMessage*  
 [輸入/輸出]On 輸入包含 *wszMessage* 緩衝區的大小（以字元為單位）。 輸出時，如果指定的緩衝區大小太小，則會包含所需的緩衝區大小 (以字元為單位)，包括尾端的 Null。 如果函數成功，則會在訊息中包含字元數，尾端的 Null 不計。  
  
## <a name="returns"></a>傳回  
 S_OK  
 此函數已成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB 未安裝在電腦上。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一個或多個指定的輸入參數無效。  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 要求的訊息不存在。  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 未提供要求語言的訊息。  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 輸入緩衝區 *wszMessage* 太短，且未要求截斷。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 發生意外錯誤。 請參閱事件記錄檔，以取得詳細資料。  
  
## <a name="remarks"></a>備註  
 如需使用 LocalDB API 的程式碼範例，請參閱 [SQL Server Express Localdb 參考](../../relational-databases/sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Express LocalDB 標頭和版本資訊](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
