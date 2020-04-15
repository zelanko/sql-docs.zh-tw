---
title: SQLSet 設定模式功能 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c36da48fa1493f61131d23a07f7a820b67ebac82
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293278"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQLSetConfigMode**設置配置模式,指示 Odbc.ini 條目清單 DSN 值在系統資訊中的位置。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>引數  
 *w 設定模式*  
 [輸入]安裝程式配置模式(請參閱"註釋")。 *wConfigMode*中的值可以是:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetConfigMode**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|不合法參數序列|*wConfigMode*參數不包含ODBC_USER_DSN、ODBC_SYSTEM_DSN 或ODBC_BOTH_DSN。|  
  
## <a name="comments"></a>註解  
 此功能用於設置 Odbc.ini 條目列表 DSN 值在系統資訊中的位置。 如果*wConfigMode* ODBC_USER_DSN,則 DSN 是使用者 DSN,函數從 odbc.ini 條目讀取HKEY_CURRENT_USER。 如果ODBC_SYSTEM_DSN,DSN 是系統 DSN,函數從 HKEY_LOCAL_MACHINE 中的 Odbc.ini 條目讀取。 如果ODBC_BOTH_DSN,則嘗試HKEY_CURRENT_USER,如果失敗,則使用HKEY_LOCAL_MACHINE。  
  
 此函數不影響**SQLCreateDataSource**和**SQLDriverConnect**。 當驅動程式透過調用**SQLGetPrivateProfileString**或透過呼叫**SQLWritePrivateProfileString**從註冊表讀取時,必須設置配置模式。 對**SQLGetPrivateProfileString**和**SQLWritePrivateProfileString**的呼叫使用配置模式來瞭解要操作的註冊表的哪個部分。  
  
> [!CAUTION]  
>  僅在必要時才應調用**SQLSet 配置模式**;如果模式設定不正確,ODBC 安裝程式可能無法正常運行。  
  
 **SQLSetConfigMode**對配置模式進行直接註冊表修改。 這與通過調用**SQLConfigDataSource**修改配置模式的過程不同。 對**SQLConfigDataSource**的調用將配置模式設定在修改 DSN 時區分使用者和系統 DSN。 在返回之前 **,SQLConfigDataSource**會將配置模式重置為 BOTHDSN。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|建立資料來源|[SQLCreate資料來源](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|使用連接字串或對話框連接到資料來源|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|檢索設定模式|[SQLGet 設定模式](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
