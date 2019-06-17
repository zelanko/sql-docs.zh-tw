---
title: 原生錯誤碼 |Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63223494"
---
# <a name="native-error-numbers"></a>原生錯誤號碼
  資料來源中發生的錯誤 (由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會傳回它所傳回的自發性錯誤號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 驅動程式所偵測到的錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會傳回自發性錯誤號碼為 0。 如需詳細的原生錯誤號碼清單的相關資訊，請參閱錯誤資料行的**sysmessages**系統資料表中的**主要**資料庫中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 有關狀態錯誤碼的資訊，請參閱[SQLSTATE &#40;ODBC 錯誤碼&#41;](sqlstate-odbc-error-codes.md)。 對於網路程式庫所傳回的錯誤，自發性錯誤號碼來自於基礎網路軟體。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](handling-errors-and-messages.md)  
  
  
