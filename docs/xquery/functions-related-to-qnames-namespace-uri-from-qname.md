---
title: 命名空間-從-QName （XQuery）開始的 uri |Microsoft Docs
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
ms.openlocfilehash: 96edefd5409520109e2b2155507dd8879ed4b0d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67946639"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>與 QNames 相關的函式 - namespace-uri-from-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回字串，代表 *$arg*所指定之 QName 的命名空間 uri。 如果 *$arg*是空的序列，則結果會是空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 是傳回其命名空間 URI 的 QName。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. 從 QName 擷取命名空間 URI  
 如需實用範例，請參閱[從 QName &#40;XQuery&#41;的本機名稱](../xquery/functions-related-to-qnames-local-name-from-qname.md)。  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Namespace-uri from-QName （）** 函數會傳回 xs： string 的實例，而不是 Xs： anyURI。  
  
## <a name="see-also"></a>另請參閱  
 [與 QNames &#40;XQuery&#41;相關的函數](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
