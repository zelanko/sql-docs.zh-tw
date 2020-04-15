---
title: 環境句柄 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b504995e99dfad032598485e370b4d5a6681ae81
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300438"
---
# <a name="environment-handles"></a>環境控制代碼
*環境*是訪問數據的全域上下文;與環境關聯的是任何全域性資訊,例如:  
  
-   環境的狀態  
  
-   目前環境級診斷  
  
-   目前在環境中分配的連線的句柄  
  
-   每個環境屬性的目前設定  
  
 在實現 ODBC(驅動程式管理器或驅動程式)的代碼段中,環境句柄標識結構以包含此資訊。  
  
 環境句柄在 ODBC 應用中不經常使用。 它們始終用於對**SQLDataSources**和**SQLDrivers 的**調用,有時用於對 SQLAllocHandle、SQLEndTran、SQLFreeHandle、SQLGetDiagField 和**SQLGetDiagRec**的調用。 **SQLAllocHandle** **SQLEndTran** **SQLFreeHandle** **SQLGetDiagField**  
  
 實現 ODBC 的每個程式碼段(驅動程式管理器或驅動程式)包含一個或多個環境句柄。 例如,驅動程式管理器為連接到它的每個應用程式維護一個單獨的環境句柄。 環境句柄使用**SQLAllocHandle**分配,並釋放**SQLFreeHandle**。
