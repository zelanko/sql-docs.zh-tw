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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036420"
---
# <a name="connection-strings"></a>連接字串
連接字串包含用來建立連接的資訊。 完整的連接字串包含建立連接所需的所有資訊。 連接字串是一系列以分號分隔的關鍵字/值配對。 （如需連接字串的完整語法，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函數描述）。連接字串的使用方式：  
  
-   **SQLDriverConnect**，它會透過與使用者互動來完成連接字串。  
  
-   **SQLBrowseConnect**，這會以資料來源反復完成連接字串。  
  
 **SQLConnect**不會使用連接字串;使用**SQLConnect**類似于使用具有三個關鍵字/值組的連接字串進行連接（適用于資料來源名稱和選擇性的使用者識別碼和密碼）。
