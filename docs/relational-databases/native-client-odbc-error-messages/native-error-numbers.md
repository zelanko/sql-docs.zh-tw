---
title: 原生錯誤號碼 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1bc1f9383ab615a24b0506b86cf0ec5e37b6c74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783403"
---
# <a name="native-error-numbers"></a>原生錯誤號碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  對於發生在資料來源中的錯誤（由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回）， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native Client ODBC 驅動程式會傳回由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回的原生錯誤號碼。 對於驅動程式所偵測到的錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，NATIVE Client ODBC 驅動程式會傳回原生錯誤號碼0。 如需原生錯誤號碼清單的詳細資訊，請參閱中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **master**資料庫內**sysmessages**系統資料表的 error 資料行。  
  
 如需狀態錯誤碼的詳細資訊，請參閱[SQLSTATE &#40;ODBC 錯誤碼&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)。 對於網路程式庫所傳回的錯誤，自發性錯誤號碼來自於基礎網路軟體。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
