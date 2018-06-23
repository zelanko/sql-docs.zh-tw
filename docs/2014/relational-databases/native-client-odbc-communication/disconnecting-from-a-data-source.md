---
title: 從資料來源中斷連線 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- disconnecting [ODBC]
- ODBC applications, disconnecting
- SQLDisconnect function
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLFreeHandle function
- ODBC data sources, disconnecting
- SQL Server Native Client ODBC driver, data sources
- ODBC functions
- SQL Server Native Client ODBC driver, connections
ms.assetid: 65b0267d-b2ab-4a59-83f2-436d90cfbf79
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 93afdf5c897525d0b3e925736e763f3da066941e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031006"
---
# <a name="disconnecting-from-a-data-source"></a>從資料來源中斷連接
  當應用程式已經完成使用資料來源時，它會呼叫**SQLDisconnect**。 **SQLDisconnect**釋放連接配置的任何陳述式，並從資料來源中斷驅動程式。 中斷連接之後，應用程式可以呼叫[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)來釋放連接控制代碼。 結束之前，應用程式也會呼叫**SQLFreeHandle**來釋放環境控制代碼。  
  
 中斷連接之後，應用程式可以重複使用配置的連接控制代碼來連接到不同的資料來源或重新連接到相同的資料來源。 選擇保持連接狀態，而非中斷連接並稍後再重新連接時，應用程式撰寫者必須考慮每個選擇的相對成本。 連接到資料來源並維持連接狀態可能相當昂貴，端視連接媒體而定。 進行取捨時，應用程式也必須假設在相同資料來源上進行額外作業的可能性和時機。 應用程式可能也必須使用多個連接。  
  
## <a name="see-also"></a>另請參閱  
 [與 SQL Server 通訊&#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  