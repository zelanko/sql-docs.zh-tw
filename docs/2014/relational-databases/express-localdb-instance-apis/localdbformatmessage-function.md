---
title: LocalDBFormatMessage 函式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBFormatMessage
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d287a7ceff1c38c829da91a8ae2e530f664fb4ef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128745"
---
# <a name="localdbformatmessage-function"></a>LocalDBFormatMessage 函數
  傳回指定之 SQL Server Express LocalDB 錯誤的當地語系化文字描述。  
  
 **標頭檔：** sqlncli.h  
  
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
 [輸入/輸出]輸入包含的大小*wszMessage*以字元為單位的緩衝區。 輸出時，如果指定的緩衝區大小太小，則會包含所需的緩衝區大小 (以字元為單位)，包括尾端的 Null。 如果函數成功，則會在訊息中包含字元數，尾端的 Null 不計。  
  
## <a name="returns"></a>傳回值  
 S_OK  
 此函數已成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB 未安裝在電腦上。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一個或多個指定的輸入參數無效。  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 要求的訊息不存在。  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 未提供要求語言的訊息。  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 輸入的緩衝區*wszMessage*太短，而且未要求截斷。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 發生意外的錯誤。 請參閱事件記錄檔，以取得詳細資料。  
  
## <a name="remarks"></a>備註  
 使用 LocalDB API 的程式碼範例，請參閱 < [SQL Server Express LocalDB 參考](../sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Express LocalDB 標頭和版本資訊](sql-server-express-localdb-header-and-version-information.md)  
  
  
