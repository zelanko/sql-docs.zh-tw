---
title: 命名空間-uri-從 QName (XQuery) |Microsoft Docs
description: 瞭解如何使用命名空間 uri-自 QName 函式來取出 QName 的命名空間 URI。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 035b92b719431b5a9b74f951f20d51911a41d59c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035770"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>與 QNames 相關的函式 - namespace-uri-from-QName
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  傳回字串，表示 *$arg*所指定之 QName 的命名空間 uri。 如果 *$arg* 是空的序列，則結果為空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 是傳回其命名空間 URI 的 QName。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種 **xml** 類型資料行中。  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. 從 QName 擷取命名空間 URI  
 如需實用的範例，請參閱 [本機名稱-從 QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md)。  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **命名空間-uri-從 QName ( # B1**函數會傳回 xs： string 的實例，而非 Xs： anyURI。  
  
## <a name="see-also"></a>另請參閱  
 [QNames &#40;XQuery&#41;的相關函數 ](./functions-related-to-qnames-expanded-qname.md)  
  
