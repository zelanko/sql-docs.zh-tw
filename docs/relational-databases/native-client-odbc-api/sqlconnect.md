---
title: SQLConnect |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLConnect function
ms.assetid: 6da74e3a-4388-4907-81cb-987389bae467
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b5440bff64349fb8125245961fddb6a54056fb91
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698649"
---
# <a name="sqlconnect"></a>SQLConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  開啟連接時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會將 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 設定為開啟連接所使用的驗證方法。 如需有關 Spn 的詳細資訊，請參閱[服務主要名稱&#40;Spn&#41;用戶端連接中&#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。  
  
## <a name="sqlconnect-support-for-high-availability-disaster-recovery"></a>高可用性/災害復原的 SQLConnect 支援  
 如需有關使用**SQLConnect**連接到[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]叢集，請參閱[SQL Server Native Client Support for High Availability，Disaster Recovery](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLConnect 函數](http://go.microsoft.com/fwlink/?LinkId=101541)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
