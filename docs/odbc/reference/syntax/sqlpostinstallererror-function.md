---
title: SQLPostInstallerError 函式 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306889"
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 函式
**標準**  
 引進的版本： ODBC 3。0  
  
 **摘要**  
 **SQLPostInstallerError**提供一個機制，讓驅動程式或 translator 安裝程式庫向安裝程式錯誤佇列報告**ConfigDriver**、 **ConfigDSN**和**ConfigTranslator**函數的錯誤。 應用程式不會使用此 API;它們會使用**SQLInstallerError**來取得錯誤。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>引數  
 *fErrorCode*  
 源安裝程式錯誤碼。  
  
 *szErrorMsg*  
 源錯誤訊息正文。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLPostInstallerError**不會為本身張貼錯誤值。 如果錯誤已成功張貼到安裝程式錯誤佇列（可使用**SQLInstallerError**來抓取），則會傳回 SQL_SUCCESS。 如果*dwErrorCode*引數中的值不是其中一個指定的安裝程式錯誤碼，則會傳回 SQL_ERROR。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|新增、修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|設定翻譯選項|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
