---
title: SQLEndTran |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f2c4851b4cbb88c0d927aa4739e06501ce5ca1b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298508"
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  預設情況下,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當**SQLEndTran**提交或回滾操作時,本機用戶端 ODBC 驅動程式將關閉語句的關聯游標。 除非伺服器資料指標是靜態的，否則會關閉它們。 當**SQLEndTran**提交或回滾操作時,語句關聯游標的行為由特定於驅動程式的 ODBC 連接屬性的值SQL_COPT_SS_PRESERVE_CURSORS由[SQLSetConnect Attr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)設置。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 進行詳細資訊](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran 函數](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
