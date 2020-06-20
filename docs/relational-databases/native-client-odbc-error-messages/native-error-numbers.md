---
title: 原生錯誤號碼 |Microsoft Docs
description: 對於錯誤，SQL Server Native Client ODBC 驅動程式會從 SQL Server 或（針對驅動程式偵測到的錯誤）傳回原生錯誤號碼，0。
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
ms.openlocfilehash: 2ced3928145fd1420dd9e1f75644befedaae3c88
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967642"
---
# <a name="native-error-numbers"></a>原生錯誤號碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  對於發生在資料來源中的錯誤（由傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ）， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會傳回由傳回的原生錯誤號碼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 對於驅動程式所偵測到的錯誤， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會傳回原生錯誤號碼0。 如需原生錯誤號碼清單的詳細資訊，請參閱中**master**資料庫內**sysmessages**系統資料表的 error 資料行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 如需狀態錯誤碼的詳細資訊，請參閱[SQLSTATE &#40;ODBC 錯誤碼&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)。 對於網路程式庫所傳回的錯誤，自發性錯誤號碼來自於基礎網路軟體。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
