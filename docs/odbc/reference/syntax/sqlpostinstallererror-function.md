---
description: SQLPostInstallerError 函式
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
ms.openlocfilehash: a041069de4c8b86946f7088d6a46462468cc3656
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487207"
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 函式
**一致性**  
 引進的版本： ODBC 3。0  
  
 **總結**  
 **SQLPostInstallerError** 提供一種機制，讓驅動程式或轉譯器安裝程式庫將 **ConfigDriver**、 **ConfigDSN**和 **ConfigTranslator** 函式的錯誤報表給安裝程式錯誤佇列。 應用程式不會使用此 API;它們使用 **SQLInstallerError** 來取出錯誤。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>引數  
 *fErrorCode*  
 輸出安裝程式錯誤碼。  
  
 *szErrorMsg*  
 輸出錯誤訊息正文。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLPostInstallerError** 不會張貼本身的錯誤值。 如果錯誤成功地張貼到安裝程式錯誤佇列 (可使用 **SQLInstallerError**) 來進行，則會傳回 SQL_SUCCESS。 如果 *dwErrorCode* 引數中的值不是其中一個指定的安裝程式錯誤碼，則會傳回 SQL_ERROR。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|新增、修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|設定轉譯選項|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
