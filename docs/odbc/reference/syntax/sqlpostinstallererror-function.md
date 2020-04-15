---
title: SQLPost安裝程式錯誤功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cdceff5c4e175ba9f135c6e5e4405933b1a86b7c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306889"
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQLPost安裝程式Error**為驅動程式或轉換器設定庫提供了一種機制,用於向安裝程式錯誤佇列報告**配置驅動程式**、**配置DSN**和**配置器函數**的錯誤。 應用程式不使用此 API;因此,應用程式不會使用此 API。他們使用**SQL 安裝程式錯誤**來檢索錯誤。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>引數  
 *fErrorCode*  
 [輸入]安裝程式錯誤代碼。  
  
 *什洛姆斯格*  
 [輸入]錯誤訊息文本。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS或SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLPost安裝程式錯誤**不會為自己發佈錯誤值。 如果錯誤已成功發佈到安裝程式錯誤佇列(使用**SQL 安裝程式錯誤**可檢索),則返回SQL_SUCCESS。 如果*dwErrorCode*參數中的值不是指定的安裝程式錯誤代碼之一,則將返回SQL_ERROR。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[設定驅動程式](../../../odbc/reference/syntax/configdriver-function.md)|  
|新增、修改或移除資料來源|[設定DSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|設定翻譯選項|[設定轉換器](../../../odbc/reference/syntax/configtranslator-function.md)|
