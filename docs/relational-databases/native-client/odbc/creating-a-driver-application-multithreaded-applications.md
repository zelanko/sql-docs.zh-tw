---
title: 多執行緒應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- threads [SQL Server], multithreaded applications
- ODBC applications, multithreaded applications
- asynchronous operations [SQL Server Native Client]
- SQL Server Native Client ODBC driver, multithreaded applications
- multithreaded applications [SQL Server Native Client]
ms.assetid: d352c91a-6e08-4e50-9f3e-a37892d9c2cc
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d557b9195e14f4546d8b003f52bebdb7f0c2065b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419497"
---
# <a name="creating-a-driver-application---multithreaded-applications"></a>建立驅動程式應用程式-多執行緒應用程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式是一個多執行緒的驅動程式。 撰寫多執行緒應用程式是使用非同步呼叫處理多個 ODBC 呼叫的替代方式。 執行緒可以進行非同步的 ODBC 呼叫，而其他執行緒可以在第一個執行緒遭到封鎖而等待回應其呼叫時處理。 此模式比進行非同步呼叫更有效率，因為它會排除網路流量之類的負擔，而且產生重複的 ODBC 函數會呼叫 SQL_STILL_EXECUTING 的測試。  
  
 非同步模式仍然是處理的有效方法。 多執行緒模型的效能改善還不足以免於重新撰寫非同步的應用程式。 如果使用者要轉換使用 DB-Library 非同步模型的 DB-Library 應用程式，將它們轉換為 ODBC 非同步模式更為容易。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SQL Server Native Client ODBC 驅動程式應用程式](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
