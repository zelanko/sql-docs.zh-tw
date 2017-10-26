---
title: "連接控制代碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba20d3fcb6d943f4669774013dcb62c8ad896d8d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connection-handles"></a>連接控制代碼
A*連接*驅動程式和資料來源所組成。 連接控制代碼識別每個連接。 連接控制代碼會定義要使用哪一個驅動程式不僅要使用該驅動程式與資料來源。 在區段程式碼會實作 ODBC （驅動程式管理員或驅動程式） 中，在連接控制代碼識別結構，其中包含連接資訊，如下所示：  
  
-   連接狀態  
  
-   目前的連接層級診斷  
  
-   陳述式與目前連接上配置描述項控制代碼  
  
-   每個連接屬性的目前的設定  
  
 ODBC 無法防止多個同時連線，如果驅動程式支援它們。 因此，在特定的 ODBC 環境中，多個連接控制代碼可能會以各種不同的驅動程式和資料來源，以相同的驅動程式和各種不同的資料來源，或甚至相同驅動程式與資料來源的多個連接點。 有些驅動程式限制支援; 使用中連接的數目SQL_MAX_DRIVER_CONNECTIONS 選項**SQLGetInfo**指定特定驅動程式支援多少作用中連線。  
  
 連接到資料來源時，主要是用連接控制代碼 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**)，正在中斷連線的資料來源 (**SQLDisconnect**)，取得的驅動程式和資料來源的相關資訊 (**SQLGetInfo**)，擷取診斷 (**SQLGetDiagField**和**SQLGetDiagRec**)，以及執行交易 (**SQLEndTran**)。 也會使用設定和取得連接屬性時 (**SQLSetConnectAttr**和**SQLGetConnectAttr**)，取得原生格式的 SQL 陳述式時 (**SQLNativeSql**).  
  
 被配置連接控制代碼**SQLAllocHandle**且已釋放與**SQLFreeHandle**。

