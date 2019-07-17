---
title: 連接字串 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to driver [ODBC], connection strings
- functions [ODBC], data source or driver connections
- connection strings [ODBC], about connection strings
- connecting to data source [ODBC], connection strings
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: 724c7b86-300a-4fa9-ad96-4afa0fdcb3e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f68a87db729df2f4a27e2766a9de60e8c75a71a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036420"
---
# <a name="connection-strings"></a>連接字串
連接字串包含用來建立連線資訊。 完整連接字串包含建立連接所需要的所有資訊。 連接字串是一系列以分號隔開的關鍵字/值組。 (如需連接字串的完整語法，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。)使用連接字串：  
  
-   **SQLDriverConnect**，這會完成與使用者互動的連接字串。  
  
-   **SQLBrowseConnect**，其完成反覆與資料來源的連接字串。  
  
 **SQLConnect**不會使用連接字串; 使用**SQLConnect**相當於連接使用連接字串包含剛好三個的關鍵字/值組 (資料來源名稱和 （選擇性） 使用者識別碼和密碼).
