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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 502a4eeb657d4bc9e92a2cda25e152329b281567
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790600"
---
# <a name="logged-vs-unlogged-modifications"></a>已記錄及未記錄的修改
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  應用程式可以要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不會記錄**text**、 **Ntext**和**image**的修改。 但是在使用這個選項時，應該要特別小心。 只有當**text**、 **Ntext**或**image**資料不重要，而且資料擁有者願意將復原資料的能力視為較高的效能時，才應該使用此功能。  
  
 **Text**、 **Ntext**和**image**修改的記錄是藉由呼叫[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) ，並將*Attribute*參數設定為 SQL_SOPT_SS_ TEXTPTR_LOGGING，並將*valueptr 是*設定為 SQL_TL_ON 或SQL_TL_OFF。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
