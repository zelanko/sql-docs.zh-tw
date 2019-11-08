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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 83785ff799ee7e530c1f403acd32f4e8f355d1eb
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787458"
---
# <a name="sqlconnect"></a>SQLConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  開啟連接時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會將 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 設定為開啟連接所使用的驗證方法。 如需 Spn 的詳細資訊，請參閱[客戶&#40;端&#41;連接&#40; &#41;ODBC 中的服務主體名稱 spn](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。  
  
## <a name="sqlconnect-support-for-high-availability-disaster-recovery"></a>高可用性/災害復原的 SQLConnect 支援  
 如需使用**SQLConnect**連線到 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 叢集的詳細資訊，請參閱[高可用性和嚴重損壞修復的 SQL Server Native Client 支援](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLConnect 函數](https://go.microsoft.com/fwlink/?LinkId=101541)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
