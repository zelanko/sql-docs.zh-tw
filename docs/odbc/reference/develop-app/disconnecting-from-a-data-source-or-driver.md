---
title: 中斷連接資料的資料來源或驅動程式 |Microsoft 文件
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
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c99a2fb7c441c6de2a229895a1a68d68e9240c7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>中斷連接資料的資料來源或驅動程式
當應用程式已經完成使用資料來源時，它會呼叫**SQLDisconnect**。 **SQLDisconnect**釋放連接配置的任何陳述式，並從資料來源中斷驅動程式。 如果交易中處理程序，它會傳回錯誤。  
  
 中斷連接之後，應用程式可以呼叫**SQLFreeHandle**來釋放連接。 釋放後連接，它是應用程式的程式設計錯誤; ODBC 函數呼叫中使用連接的控制代碼這樣做，因此必須未定義，但可能是嚴重的後果。 當**SQLFreeHandle**呼叫時，結構用來儲存連接資訊的驅動程式版本。  
  
 應用程式也可以重複使用的連接，以連接到不同的資料來源或重新連線到相同的資料來源。 選擇保持連接，而非中斷並重新連接之後，需要應用程式寫入器，考慮每個選項; 相對成本同時連接到資料來源並維持連接狀態可以是相當耗成本視連接媒體而定。 在正確的權衡取捨時，應用程式也必須進行的可能性和時機未來在相同的資料來源上的操作的相關假設。
