---
title: 本機錯誤編號 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b5572ee784f47b0444e1d825de1b6dd53db8066
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291602"
---
# <a name="native-error-numbers"></a>原生錯誤號碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  對於資料源中發生的錯誤(返回者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]),本機用戶端ODBC驅動程式返回返回的本機錯誤編號[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 對於驅動程式檢測到的錯誤,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式傳回本機錯誤數 0。 有關本機錯誤編號清單的詳細資訊,請參閱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的**主**資料庫中**系統**表的錯誤列。  
  
 有關狀態錯誤代碼的資訊,請參閱[SQLSTATE &#40;ODBC 錯誤代碼&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)。 對於網路程式庫所傳回的錯誤，自發性錯誤號碼來自於基礎網路軟體。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
