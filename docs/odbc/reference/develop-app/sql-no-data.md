---
title: SQL_NO_DATA |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a399a270eb1cd2f3daf9449c53b1f577a6b9545
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299788"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
當一個ODBC 3。*x*應用程式在 ODBC 2 中呼叫**SQLExecDirect、SQLExecute**或**SQLExecute****SQLParamData。***x*驅動程式執行不影響數據源上任何行的搜索更新或刪除語句,驅動程式應返回SQL_SUCCESS,而不是SQL_NO_DATA。 當一個ODBC 2。*x*或 ODBC 3。*x*使用 ODBC 3 的應用程式。*x*驅動程式呼叫**SQLExecDirect、SQLExecute**或**SQLExecute****SQLParamData,** 其結果相同,即 ODBC 3。*x*驅動程式應返回SQL_NO_DATA。
