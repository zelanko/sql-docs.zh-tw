---
title: 第 6 步:斷開與數據源的連接 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df8cd94435d74bf813b0b64be0753a0beb44d354
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302789"
---
# <a name="step-6-disconnect-from-the-data-source"></a>步驟 6：中斷與資料來源的連線
最後一步是斷開與數據源的連接,如下圖所示。 首先,應用程式通過調用**SQLFreeHandle**釋放任何語句句柄。 有關詳細資訊,請參閱[釋放語句句柄](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 ![顯示中斷連接資料來源](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 接下來,應用程式使用**SQLDisconnect**與資料源斷開連接,並釋放**SQLFreeHandle**的連接句柄。 有關詳細資訊,請參閱[斷開與數據源或驅動程式](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)的連接。  
  
 最後,應用程式使用**SQLFreeHandle**釋放環境句柄並卸載驅動程式管理器。 有關詳細資訊,請參閱[分配環境句柄](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。
