---
title: 原生錯誤號碼 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: faee9067ccf8f60a4b7dade849a0a987b5c07bd0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131939"
---
# <a name="native-error-numbers"></a>原生錯誤號碼
  資料來源中發生的錯誤 (由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會傳回它所傳回的自發性錯誤號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 驅動程式所偵測到錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會傳回自發性錯誤號碼為 0。 原生錯誤號碼清單的相關資訊，請參閱錯誤資料行的**sysmessages**系統資料表中的**主要**資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 有關狀態錯誤碼的詳細資訊，請參閱[SQLSTATE &#40;ODBC 錯誤碼&#41;](sqlstate-odbc-error-codes.md)。 對於網路程式庫所傳回的錯誤，自發性錯誤號碼來自於基礎網路軟體。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](handling-errors-and-messages.md)  
  
  