---
title: SQLNumResultCols |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0eb6de956884eb66990459b8b4c6a6336c8ed8ac
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705946"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  對於執行的語句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式不會造訪伺服器來報告結果集中的資料行數目。 在此情況下， `SQLNumResultCols` 並不會造成伺服器往返。 如同[SQLDescribeCol](sqldescribecol.md)和[SQLColAttribute](sqlcolattribute.md)， `SQLNumResultCols` 在已備妥但未執行的語句上呼叫，會產生伺服器往返。  
  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式批次傳回多個結果資料列集時，結果集資料行的數目有可能從某個資料列集變成另一個資料列集。 `SQLNumResultCols`應針對每個集合呼叫。 當資料行數目變更時，應用程式應該在提取資料列結果以前先重新繫結資料值。 如需有關處理多個結果集傳回的詳細資訊，請參閱[SQLMoreResults](sqlmoreresults.md)。  
  
 從開始，database engine 的改進 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可讓 SQLNumResultCols 取得預期結果的更精確描述。 這些更精確的結果可能與舊版的 SQLNumResultCols 所傳回的值不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[中繼資料探索](../native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLNumResultCols 函式](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
