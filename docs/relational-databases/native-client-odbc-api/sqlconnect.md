---
title: SQLConnect |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLConnect function
ms.assetid: 6da74e3a-4388-4907-81cb-987389bae467
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 46ec2436b2a79b63a7e7fd5274334c3cc8b9e0f7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789355"
---
# <a name="sqlconnect"></a>SQLConnect
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  開啟連接時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會將 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 設定為開啟連接所使用的驗證方法。 如需 Spn 的詳細資訊，請參閱[&#40;ODBC&#41;的用戶端連接中 &#40;spn&#41; 的服務主體名稱](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。  
  
## <a name="sqlconnect-support-for-high-availability-disaster-recovery"></a>高可用性/災害復原的 SQLConnect 支援  
 如需使用**SQLConnect**連線到叢集的詳細資訊 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ，請參閱[高可用性和嚴重損壞修復 SQL Server Native Client 支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLConnect 函式](https://go.microsoft.com/fwlink/?LinkId=101541)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
