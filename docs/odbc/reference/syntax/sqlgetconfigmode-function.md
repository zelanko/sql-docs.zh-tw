---
title: SQLGet 設定模式功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc11bec24ede3352dd43f3645fb8c720b77fdabe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285688"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQLGetConfigMode**檢索指示 Odbc.ini 條目列表 DSN 值在系統資訊中的位置的配置模式。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>引數  
 *pwConfigmode*  
 【輸出]指向包含配置模式的緩衝區的指標。 (請參閱"註釋」。。* \*pwConfigMode*中的值可以是:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetConfigMode**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 此功能用於確定 Odbc.ini 條目列表 DSN 值在系統資訊中的位置。 如果*\*pwConfigMode* ODBC_USER_DSN,則 DSN 是使用者 DSN,函數從 HKEY_CURRENT_USER 中的 Odbc.ini 條目讀取。 如果ODBC_SYSTEM_DSN,DSN 是系統 DSN,函數從 HKEY_LOCAL_MACHINE 中的 Odbc.ini 條目讀取。 如果ODBC_BOTH_DSN,則嘗試HKEY_CURRENT_USER,如果失敗,則使用HKEY_LOCAL_MACHINE。  
  
 默認情況下 **,SQLGet ConfigMode**返回ODBC_BOTH_DSN。 當使用者 DSN 或系統 DSN 透過呼叫**SQLConfigDataSource**創建時,該函數將配置模式設定為ODBC_USER_DSN或ODBC_SYSTEM_DSN,以在修改 DSN 時區分使用者和系統 DSN。 在返回之前 **,SQLConfigDataSource**會將配置模式重置為ODBC_BOTH_DSN。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|設定組態模式|[SQLSet 設定模式](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
