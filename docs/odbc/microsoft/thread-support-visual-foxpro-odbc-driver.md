---
title: 線程支援(可視化福克斯Pro ODBC驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aa19eb233525b5a65ef67fe9903814fc1163177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303079"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>執行緒支援 (Visual FoxPro ODBC Driver)
可視化 FoxPro ODBC 驅動程式是線程安全的。 對環境句柄 (*hen)、* 連接句柄 (*hdbc*) 和語句句柄 (*hstmt*) 的訪問被包裝在適當的訊號量中,以防止其他行程存取並可能更改驅動程式的內部資料結構。  
  
 在多線程應用程式中,可以通過在單獨的線程上調用[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)來取消在*hstmt*上同步運行的函數。  
  
 使用漸進式提取時,驅動程式使用單獨的線程來獲取數據。 要對資料來源使用逐行提取,請在[ODBC Visual FoxPro 安裝程式對話框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)**的後台複選框中選擇「提取資料**」,或在連接字串中使用後臺提取屬性關鍵字。 避免在從多線程應用程式調用驅動程式時使用後臺提取。 有關連接字串屬性關鍵字的資訊,請參閱[使用連接字串](../../odbc/microsoft/using-connection-strings.md)。  
  
 有關線程和**SQLCancel**的詳細資訊,請參閱*ODBC 程式師參考*中的[SQLCancel。](../../odbc/reference/syntax/sqlcancel-function.md)
