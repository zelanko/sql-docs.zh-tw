---
title: 配置環境控制代碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66afa14ccb1953265f526f8c8861237638f569fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199039"
---
# <a name="allocating-an-environment-handle"></a>配置環境控制代碼
  應用程式必須先初始化 ODBC 環境並配置環境控制代碼，然後才能呼叫任何 ODBC 函數。 在 ODBC 中，這是其他控制代碼的全域內容控制代碼和預留位置。 您可以呼叫**SQLAllocHandle**具有*HandleType*參數設定為 SQL_HANDLE_ENV 並*InputHandle*設定為 SQL_NULL_HANDLE。  
  
 配置環境控制代碼之後，應用程式必須設定環境屬性來指出它將使用的 ODBC 函數呼叫版本。 若要使用 ODBC 3。*x*函式，呼叫[SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)具有*屬性*參數設定為 SQL_ATTR_ODBC_VERSION 並*ValuePtr*設 SQL_OV_ODBC3。  
  
## <a name="see-also"></a>另請參閱  
 [與 SQL Server 通訊&#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
