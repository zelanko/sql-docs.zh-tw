---
title: 多執行緒應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- threads [SQL Server], multithreaded applications
- ODBC applications, multithreaded applications
- asynchronous operations [SQL Server Native Client]
- SQL Server Native Client ODBC driver, multithreaded applications
- multithreaded applications [SQL Server Native Client]
ms.assetid: d352c91a-6e08-4e50-9f3e-a37892d9c2cc
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e7a2a778f4af4c39e53942401e0de93997afbb64
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73761255"
---
# <a name="creating-a-driver-application---multithreaded-applications"></a>建立驅動程式應用程式 - 多執行緒應用程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式是一個多執行緒的驅動程式。 撰寫多執行緒應用程式是使用非同步呼叫處理多個 ODBC 呼叫的替代方式。 執行緒可以進行非同步的 ODBC 呼叫，而其他執行緒可以在第一個執行緒遭到封鎖而等待回應其呼叫時處理。 此模式比進行非同步呼叫更有效率，因為它會排除網路流量之類的負擔，而且產生重複的 ODBC 函數會呼叫 SQL_STILL_EXECUTING 的測試。  
  
 非同步模式仍然是處理的有效方法。 多執行緒模型的效能改善還不足以免於重新撰寫非同步的應用程式。 如果使用者要轉換使用 DB-Library 非同步模型的 DB-Library 應用程式，將它們轉換為 ODBC 非同步模式更為容易。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SQL Server Native Client ODBC 驅動程式應用程式](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
