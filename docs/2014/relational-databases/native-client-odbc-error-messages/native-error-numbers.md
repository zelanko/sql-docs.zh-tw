---
title: 原生錯誤號碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 7e7cd24a3eb1ccdeea1b6e6cbb97e2d0f222193f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63223494"
---
# <a name="native-error-numbers"></a>原生錯誤號碼
  對於發生在資料來源中的錯誤（由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回）， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native Client ODBC 驅動程式會傳回由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回的原生錯誤號碼。 對於驅動程式所偵測到的錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，NATIVE Client ODBC 驅動程式會傳回原生錯誤號碼0。 如需原生錯誤號碼清單的詳細資訊，請參閱中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **master**資料庫內**sysmessages**系統資料表的 error 資料行。  
  
 如需狀態錯誤碼的詳細資訊，請參閱[SQLSTATE &#40;ODBC 錯誤碼&#41;](sqlstate-odbc-error-codes.md)。 對於網路程式庫所傳回的錯誤，自發性錯誤號碼來自於基礎網路軟體。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](handling-errors-and-messages.md)  
  
  
