---
description: 從資料來源或驅動程式中斷連線
title: 從資料來源或驅動程式中斷連接 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc14ca0ebf29a2ab203a4408db4b5681ad667497
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476690"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>從資料來源或驅動程式中斷連線
當應用程式完成使用資料來源時，它會呼叫 **SQLDisconnect**。 **SQLDisconnect** 會釋出連接上配置的任何語句，並中斷驅動程式與資料來源的連接。 如果交易正在處理中，則會傳回錯誤。  
  
 中斷連接之後，應用程式可以呼叫 **SQLFreeHandle** 來釋放連線。 釋放連接之後，就會發生應用程式程式設計錯誤，以在呼叫 ODBC 函數時使用連接的控制碼;這樣做會有未定義但可能會產生嚴重的後果。 呼叫 **SQLFreeHandle** 時，驅動程式會釋出用來儲存連接相關資訊的結構。  
  
 應用程式也可以重複使用連接，以連接至不同的資料來源，或重新連接到相同的資料來源。 要保持連線的決策，而不是稍後中斷連接再重新連線，應用程式撰寫者必須考慮每個選項的相對成本;連接到資料來源和剩餘的連接，都可能相當昂貴，視連接媒體而定。 在進行正確的取捨時，應用程式也必須對相同的資料來源進行進一步作業的可能性和時間假設。
