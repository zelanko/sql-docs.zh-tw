---
description: 使用伺服器資料指標
title: 使用伺服器資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e282ca10124b83956626933867f287be38b001f9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423920"
---
# <a name="using-server-cursors"></a>使用伺服器資料指標
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  如果 ODBC 應用程式將任何 ODBC 資料指標屬性設定為預設值以外的任何值，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會要求伺服器執行相同類型的 API 伺服器資料指標。 使用 API 伺服器資料指標可以釋放用戶端上的記憶體，而且可以大幅降低用戶端與伺服器之間的網路流量。  
  
 API 伺服端資料指標的潛在缺點是目前不支援所有 SQL 陳述式。 API 伺服端資料指標無法用來執行：  
  
-   傳回多個結果集的批次或預存程序。  
  
-   包含 COMPUTE、COMPUTE BY、FOR BROWSE 或 INTO 子句的 SELECT 陳述式。  
  
-   參考遠端預存程序的 EXECUTE 陳述式。  
  
 連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體時，使用伺服器資料指標執行包含這些特性的陳述式會使資料指標轉換為預設的結果集。 連接到舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，它會導致錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [如何實作資料指標](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
