---
title: 連接字串 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbbb5b4672a8ea393380063887cfd77b3e910238
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299028"
---
# <a name="connection-strings"></a>連接字串
連接字串包含用於建立連接的資訊。 完整的連接字串包含建立連接所需的所有資訊。 連接字串是一系列關鍵字/值對,由分號分隔。 (有關連接字串的完整語法,請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函數說明。連接字串由以下者使用:  
  
-   **SQLDriverConnect**,它透過與使用者的互動完成連接字串。  
  
-   **SQLBrowseConnect**,它與數據源以反覆運算方式完成連接字串。  
  
 SQLConnect 不使用連接字串;因此 **,SQLConnect**不使用連接字串。使用**SQLConnect**類似於使用僅包含三個關鍵字/ 值對的連接字串(對於資料來源名稱,可選為使用者 ID 和密碼)。
