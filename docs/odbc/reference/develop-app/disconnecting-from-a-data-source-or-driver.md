---
title: 正在中斷連接的資料來源或驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2189c0fcc65fd4192e94da140e2d55ac86826137
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706416"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>從資料來源或驅動程式中斷連線
當應用程式完成使用資料來源時，它會呼叫**SQLDisconnect**。 **SQLDisconnect**釋放連接配置的任何陳述式，並從資料來源中斷驅動程式。 如果交易正在處理中，它會傳回錯誤。  
  
 中斷連接之後，應用程式可以呼叫**SQLFreeHandle**來釋放連接。 釋出連線，之後應用程式的程式設計錯誤的 ODBC 函式; 呼叫中使用的連接控制代碼如此一來，所以都未定義，但可能嚴重的後果。 當**SQLFreeHandle**會呼叫結構用來儲存連線資訊的驅動程式版本。  
  
 應用程式也可以重複使用的連接，連接到不同的資料來源，或是重新連線到相同的資料來源。 決定来保持連接，而不中斷連線或重新連線之後，需要應用程式寫入器，請考慮每個選項; 的相對成本同時連接到資料來源，並維持連接狀態可以是相當耗成本，視連接媒體而定。 在正確的權衡取捨時，應用程式也必須進行假設可能性並進一步作業相同的資料來源上的時間。
