---
title: 連接字串 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8916e4389e40959c490ab67af48661d20ee1d2cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connection-strings"></a>連接字串
連接字串包含用來建立連接的資訊。 完整的連接字串包含建立連接所需要的所有資訊。 連接字串是一系列以分號隔開的關鍵字/值組。 (如連接字串的完整語法，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。)使用連接字串：  
  
-   **SQLDriverConnect**，這會透過使用者互動來完成連接字串。  
  
-   **SQLBrowseConnect**，其完成反覆與資料來源的連接字串。  
  
 **SQLConnect**不會使用連接字串，使用**SQLConnect**類似連接使用連接字串具有三個關鍵字/值組 (資料來源名稱並選擇性地使用者 ID 和密碼).
