---
title: 連接手柄 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5b03e0733e35984350d2a218b885dc148ca8f8f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299018"
---
# <a name="connection-handles"></a>連線控制代碼
*連接*由驅動程式和數據源組成。 連接句柄標識每個連接。 連接句柄不僅定義要使用的驅動程式,還定義要與該驅動程式一起使用哪個數據源。 在實現 ODBC 的程式碼段(驅動程式管理員或驅動程式)中,連接句柄識別包含連接資訊的結構,如下所示:  
  
-   連線的狀態  
  
-   目前連線層診斷  
  
-   目前在連接上配置的敘述和描述符的句柄  
  
-   每個連線屬性的目前設定  
  
 如果驅動程式支援多個同時連接,ODBC 不會阻止它們。 因此,在特定 ODBC 環境中,多個連接句柄可能指向各種驅動程式和數據源、同一驅動程式和各種數據來源,甚至指向到同一驅動程式和數據源的多個連接。 某些驅動程式限制其支援的活動連接數;**SQLGetInfo**中的SQL_MAX_DRIVER_CONNECTIONS選項指定特定驅動程式支援多少個活動連接。  
  
 連接句柄主要用於連接到資料來源 **(SQLConnect,** **SQLDriverConnect**) 或**SQLBrowseConnect**),斷開與資料來源 **(SQLDisconnect)** 的連接),獲取有關驅動程式和資料源 **(SQLGetInfo)** 的資訊),檢索診斷 **(SQLGetDiagField**和**SQLGetDiagRec)** 和執行事務 **(SQLEndTran)。** 它們在設置和獲取連接屬性 **(SQLSetConnectAttr**和**SQLGetConnect Attr**) 以及獲取 SQL 語句 (**SQLNativeSql**) 的本機格式時也使用。  
  
 連接句柄使用**SQLAllocHandle**分配,並釋放**SQLFreeHandle**。
