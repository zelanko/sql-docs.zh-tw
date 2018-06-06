---
title: 命名空間 uri-從-QName (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 67475f0f7e10f8d49e4adefab8b44c2d4cefc272
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>函式與 QNames 相關的命名空間 uri-從-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回字串，代表所指定之 QName 的命名空間 uri *$arg*。 結果是空的序列，如果 *$arg*是空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 是傳回其命名空間 URI 的 QName。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型 AdventureWorks 資料庫中的資料行。  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. 從 QName 擷取命名空間 URI  
 如需實用範例，請參閱[本機名稱-從-QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md)。  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Namespace-uri-from-qname （)** 函式會傳回 xs: string，而不是 xs: anyuri 的執行個體。  
  
## <a name="see-also"></a>另請參閱  
 [函式與 QNames 相關的&#40;XQuery&#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
