---
title: 呼叫 SQLGetDiagField |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2ef69704ae6984f41080aea009f17ac09bafefd2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68134982"
---
# <a name="calling-sqlgetdiagfield"></a>呼叫 SQLGetDiagField
當 odbc 3.x*應用程式**呼叫 odbc 2.x*驅動程式中的**SQLGetDiagField**時，如果*以*引數是 SQL_DIAG_CLASS_ORIGIN、SQL_DIAG_CLASS_SUBCLASS_ORIGIN、SQL_DIAG_CONNECTION_NAME、SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_NUMBER、SQL_DIAG_RETURNCODE、SQL_DIAG_SERVER_NAME 或 SQL_DIAG_SQLSTATE，驅動程式將會傳回 SQL_SUCCESS 和* \*DiagInfoPtr*中的適當資訊。 所有其他診斷欄位都會傳回 SQL_ERROR。
