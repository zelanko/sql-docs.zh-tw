---
title: SQL 刪除Snfromini函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 848e82741954ab24941d5d519699292727ca25d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301797"
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 函式
**一致性**  
 版本介紹: ODBC 1.0  
  
 **摘要**  
 **SQLRemoveDSNFromIni**從系統資訊中刪除數據源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 [輸入]要刪除的資料來源的名稱。  
  
## <a name="returns"></a>傳回值  
 如果函數刪除資料來源或資料來源不在 Odbc.ini 檔中,則該函數將傳回 TRUE。 如果無法刪除數據源,它將返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDSNFromini**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_DSN|不合法的 DSN|*lpszDSN*參數無效。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|安裝程式無法從註冊表中刪除 DSN 資訊。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDSNFromIni**從系統資訊的 [ODBC 資料來源] 部分中刪除數據源名稱。 它還從系統資訊中刪除數據源規範部分。  
  
 應僅從驅動程式設置庫調用此功能。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除資料來源|[設定DSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|新增、修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|移除預設資料來源|[SQL 移除預設資料來源](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|新增資料來源名稱|[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
