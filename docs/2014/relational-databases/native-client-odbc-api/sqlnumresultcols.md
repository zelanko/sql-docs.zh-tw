---
title: SQLNumResultCols |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 73ac3425eab1a4c19130352ef566153eb6c34e53
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030038"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  對於執行的陳述式， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不會造訪伺服器來報告結果集中的資料行數目。 在此情況下，`SQLNumResultCols`不會造成伺服器往返。 像[SQLDescribeCol](sqldescribecol.md)和[SQLColAttribute](sqlcolattribute.md)，則呼叫`SQLNumResultCols`上備妥但未執行的陳述式會產生伺服器往返。  
  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式批次傳回多個結果資料列集時，結果集資料行的數目有可能從某個資料列集變成另一個資料列集。 `SQLNumResultCols` 應該針對每個集呼叫。 當資料行數目變更時，應用程式應該在提取資料列結果以前先重新繫結資料值。 如需有關處理多個結果集傳回，請參閱[SQLMoreResults](sqlmoreresults.md)。  
  
 開始 database engine 中的增強功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允許 SQLNumResultCols 以取得更精確的預期結果的描述。 這些更精確的結果，在舊版的 SQLNumResultCols 傳回的值可能會有所不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱[中繼資料探索](../native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLNumResultCols 函數](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  