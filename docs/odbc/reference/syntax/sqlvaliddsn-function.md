---
title: SQLValidDSN 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbd8df72bcb0e76c8abcc3d738c2ff8da61a7bfe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039480"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 函式
**合規性**  
 導入的版本：ODBC 2.0  
  
 **摘要**  
 **SQLValidDSN**名稱新增至 系統資訊之前會檢查長度和有效的資料來源的名稱。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 [輸入]要檢查名稱的資料來源。  
  
## <a name="returns"></a>傳回值  
 如果資料來源名稱無效，函式會傳回 TRUE。 如果資料來源名稱無效，或函式呼叫失敗，它會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLValidDSN**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 A  *\*pfErrorCode*會傳回只函式呼叫失敗時，不傳回 FALSE，因為資料來源名稱無效。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 **SQLValidDSN**驅動程式會呼叫[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)檢查資料來源名稱的長度，以及資料來源名稱中的個別字元的有效性。 它會檢查名稱的長度是否大於 SQL_MAX_DSN_LENGTH，Sqlext.h 中所定義。 (也會藉由檢查資料來源名稱的長度[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)。)**SQLValidDSN**會檢查任何下列無效的字元是否包含在資料來源名稱：  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) （在安裝程式 DLL 中）|  
|新增、 修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|系統資訊寫入資料來源名稱|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
