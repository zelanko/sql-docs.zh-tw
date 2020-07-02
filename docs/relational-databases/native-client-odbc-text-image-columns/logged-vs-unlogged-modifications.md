---
title: 已記錄與未記錄的修改 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 922d4c7be51e92b02ea904d5b4917f7ccbeec28c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760617"
---
# <a name="logged-vs-unlogged-modifications"></a>已記錄與未記錄的修改
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  應用程式可以要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式不會記錄**text**、 **Ntext**和**image**修改。 但是在使用這個選項時，應該要特別小心。 只有當**text**、 **Ntext**或**image**資料不重要，而且資料擁有者願意將復原資料的能力視為較高的效能時，才應該使用此功能。  
  
 **Text**、 **Ntext**和**image**修改的記錄是藉由呼叫[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) ，並將*Attribute*參數設定為 SQL_SOPT_SS_ TEXTPTR_LOGGING，並將*valueptr 是*設定為 SQL_TL_ON 或 SQL_TL_OFF 來控制。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
