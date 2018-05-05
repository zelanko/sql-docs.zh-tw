---
title: 使用 Microsoft 分散式交易協調器 (ODBC) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MS DTC, using
ms.assetid: 12a275e1-8c7e-436d-8a4e-b7bee853b35c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5e317fca877059bfbd1da8120a3bad3d5b2c2aab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>使用 Microsoft 分散式交易協調器 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>若要使用 MS DTC 來更新兩個或多個 SQL Server  
  
1.  使用 MS DTC OLE DtcGetTransactionManager 函數來連接至 MS DTC。 如需有關 MS DTC 的詳細資訊，請參閱 Microsoft 分散式交易協調器。  
  
2.  針對您要建立的每一個 Microsoft® SQL Server™ 連接，呼叫一次 SQL DriverConnect。  
  
3.  呼叫 MS DTC OLE ITransactionDispenser::BeginTransaction 函數來開始 MS DTC 交易並取得代表此交易的交易物件。  
  
4.  針對您想要在 MS DTC 交易中編列的每個 ODBC 連接，呼叫 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 一次或多次。 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 第二個參數必須是 SQL_ATTR_ENLIST_IN_DTC，且第三個參數必須是交易物件 (在步驟 3 中取得)。  
  
5.  針對您想要更新的每個 SQL Server，呼叫 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) 一次。  
  
6.  呼叫 MS DTC OLE ITransaction::Commit 函數來認可 MS DTC 交易。 此時，交易物件便不再有效。  
  
 若要執行一連串 MS DTC 交易，請重複步驟 3 到 6。  
  
 若要釋放交易物件的參考，請呼叫 MS DTC OLE ITransaction::Return 函數。  
  
 若要使用 ODBC 連接搭配 MS DTC 交易，然後使用相同的連接搭配本機 SQL Server 交易，請使用 SQL_DTC_DONE 來呼叫 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
> [!NOTE]  
>  您也可以針對每個 SQL Server 依序呼叫 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 和 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399)，而非依照先前步驟 4 和 5 所建議的方式呼叫它們。  
  
## <a name="see-also"></a>另請參閱  
 [執行的交易 & #40; ODBC & #41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
