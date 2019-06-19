---
title: 連接控制代碼 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77fdb63f346ada40346544a53c3ff69db0a8a9a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280846"
---
# <a name="connection-handles"></a>連線控制代碼
A*連線*驅動程式和資料來源所組成。 連接控制代碼識別每個連線。 連接控制代碼會定義要使用哪一個驅動程式不僅要搭配使用該驅動程式與資料來源。 在一段程式碼來實作 ODBC （驅動程式管理員或驅動程式），連接控制代碼會識別結構，其中包含連接資訊，如下所示：  
  
-   連接的狀態  
  
-   目前的連接層級診斷  
  
-   陳述式與目前連接上配置描述項控制代碼  
  
-   目前的設定，每個連線屬性  
  
 ODBC 不能防止多個同時連線，如果驅動程式支援它們。 因此，在特定的 ODBC 環境中，多個連接控制代碼可能會指向各種不同的驅動程式和資料來源，以相同的驅動程式和各種不同的資料來源，或甚至是相同的驅動程式與資料來源的多個連線。 有些驅動程式限制它們支援; 的作用中連線數目選項 SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo**指定特定的驅動程式支援多少個作用中連線。  
  
 連接到資料來源時，主要用於連接控制代碼 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**)、 中斷資料來源 (**SQLDisconnect**)，取得的驅動程式和資料來源的相關資訊 (**SQLGetInfo**)，擷取診斷 (**SQLGetDiagField**和**SQLGetDiagRec**)，以及執行交易 (**SQLEndTran**)。 也會使用當設定和取得的連接屬性 (**SQLSetConnectAttr**並**SQLGetConnectAttr**) 和取得的 SQL 陳述式的原生格式時 (**SQLNativeSql**).  
  
 被配置連接控制代碼**SQLAllocHandle**和與釋放**SQLFreeHandle**。
