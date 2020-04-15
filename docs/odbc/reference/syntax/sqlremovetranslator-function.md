---
title: SQL刪除轉換器功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 348d2c5da0731ba88ccd4dd6406d3754890f7906
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301785"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQLRemove 翻譯器**從系統資訊的 Odbcinst.ini 部分中刪除有關轉換器的資訊,並將轉換器的元件使用量計數減少 1。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpsz 翻譯*  
 [輸入]在系統資訊的 Odbcinst.ini 密鑰中註冊的翻譯人員的姓名。  
  
 *lpdwUsage( M) Counts*  
 【輸出]呼叫此函數後轉換器的使用計數。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。 如果在調用此函數時系統資訊中不存在條目,則函數將返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemove 轉換器**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式獲取**關聯的*\*pfError 程式*。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|註冊表中找不到元件|安裝程式無法刪除轉換器資訊,因為它要麼不存在在註冊表中,要麼在註冊表中找不到。|  
|ODBC_ERROR_INVALID_NAME|不合法的驅動程式或翻譯者名稱|*lpsz 轉換器*參數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法增加或遞減元件使用量計數|安裝程式未能減少驅動程式的使用計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLRemove 轉換器**補充[SQLInstall 翻譯器Ex](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)功能,並更新系統資訊中的元件使用方式計數。 應僅從設置應用程式調用此功能。  
  
 **SQLRemove 轉換器**將元件使用計數減少 1。 如果元件使用計數為 0,則系統資訊中的轉換器條目將被刪除。 轉換器項目位於系統資訊中的以下位置,以轉換器名稱命名:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemove 轉換器**實際上不會刪除任何檔。 呼叫程式負責刪除檔案和維護檔案使用方式計數。 只有在元件使用計數和檔使用計數都達到零后,才會物理刪除檔。 元件中的某些檔可以刪除,而其他檔不會刪除,具體取決於其他應用程式是否使用檔案,這些應用程式增加了檔使用量計數。  
  
 **SQLRemove 轉換器**也稱為升級過程的一部分。 如果應用程式檢測到必須執行升級,並且以前已安裝驅動程式,則應刪除驅動程式,然後重新安裝驅動程式。 應首先調用**SQLRemove 轉換器**來遞減元件使用計數,然後調用**SQLInstall 翻譯器 Ex**以增加元件使用計數。 應用程式安裝程式必須用新檔案物理替換舊檔。 檔使用方式計數將保持不變,使用舊版本檔的其他應用程式現在將使用較新版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|安裝翻譯器|[SQL安裝翻譯器Ex](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
