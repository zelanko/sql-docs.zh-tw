---
title: 模組和初構 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
ms.assetid: 0f17b4a4-6234-41d4-a996-6db4e27bff7e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b0300778cd850ebc13c11e3a24f738dd3f3c3573
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713116"
---
# <a name="modules-and-prologs-xquery"></a>模組和初構 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)是一系列的命名空間宣告。 在初構中使用宣告命名空間時，您可以指定命名空間繫結的前置詞並在查詢本文中使用該前置詞。  
  
## <a name="implementation-limitations"></a>實作限制  
 下列的 XQuery 規格在此實作中不受支援：  
  
-   模組宣告 (`version`)  
  
-   模組宣告 (`module namespace`)  
  
-   Xmpspacedeclaration (`xmlspace`)  
  
-   預設定序宣告 (`declare default collation`)  
  
-   基底 URI 宣告 (`declare base-uri`)  
  
-   建構宣告 (`declare construction`)  
  
-   預設排序宣告 (`declare ordering`)  
  
-   結構描述匯入 (`import schema namespace`)  
  
-   模組匯入 (`import module`)  
  
-   初構中的變數宣告 (`declare variable`)  
  
-   函數宣告 (`declare function`)  
  
## <a name="in-this-section"></a>本節內容  
 [XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)  
 描述 XQuery 初構。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
