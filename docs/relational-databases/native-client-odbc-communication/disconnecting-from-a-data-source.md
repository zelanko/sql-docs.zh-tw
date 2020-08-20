---
description: 從資料來源中斷連接
title: 中斷與資料來源的連線 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5a88b2488cbc64e77d0bcc00e3a9f758ab0f4f47
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486892"
---
# <a name="disconnecting-from-a-data-source"></a>從資料來源中斷連接
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  當應用程式完成使用資料來源時，它會呼叫 **SQLDisconnect**。 **SQLDisconnect** 會釋出連接上配置的任何語句，並中斷驅動程式與資料來源的連接。 中斷連接之後，應用程式可以呼叫 [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 來釋放連接控制碼。 在結束之前，應用程式也會呼叫 **SQLFreeHandle** 來釋放環境控制碼。  
  
 中斷連接之後，應用程式可以重複使用配置的連接控制代碼來連接到不同的資料來源或重新連接到相同的資料來源。 選擇保持連接狀態，而非中斷連接並稍後再重新連接時，應用程式撰寫者必須考慮每個選擇的相對成本。 連接到資料來源並維持連接狀態可能相當昂貴，端視連接媒體而定。 進行取捨時，應用程式也必須假設在相同資料來源上進行額外作業的可能性和時機。 應用程式可能也必須使用多個連接。  
  
## <a name="see-also"></a>另請參閱  
 [與 SQL Server &#40;ODBC&#41;通訊 ](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
