---
title: 搭配 FOR XML 使用 PATH 模式 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- PATH FOR XML mode
- characters [SQL Server], XML
- aliases [SQL Server], XML
- FOR XML clause, PATH mode
- FOR XML PATH mode
- column names [SQL Server]
- XPath queries [SQL Server]
ms.assetid: a685a9ad-3d28-4596-aa72-119202df3976
caps.latest.revision: 44
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e184fc7502af6174eef5cac8cd2914737841bb7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131663"
---
# <a name="use-path-mode-with-for-xml"></a>搭配 FOR XML 使用 PATH 模式
  如 [使用 FOR XML 建構 XML](for-xml-sql-server.md)所述，PATH 模式提供比較簡單的方式來混合元素與屬性。 PATH 模式也是導入其他巢狀以代表複雜屬性的較簡單方式。 您可以使用 FOR XML EXPLICIT 模式查詢來建構從資料列集而來的這類 XML，但是 PATH 模式對於可能會比較繁雜的 EXPLICIT 模式查詢提供較簡單的替代方案。 PATH 模式還可撰寫巢狀 FOR XML 查詢及 TYPE 指示詞，以傳回 **xml** 類型執行個體，這將可讓您撰寫較不複雜的查詢。  
  
 在 PATH 模式中，資料行名稱或資料行別名是被視為 XPath 運算式。 這些運算式指出值如何對應至 XML。 每個 XPath 運算式都是提供項目類型的相對 XPath，這些項目類型包括屬性、元素、純量值、將會產生與資料列元素相對的節點名稱與階層。  
  
 本章節描述各種條件下資料列集中的對應資料行，並提供範例。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [沒有名稱的資料行](columns-without-a-name.md)  
  
-   [有名稱的資料行](columns-with-a-name.md)  
  
-   [以萬用字元 (*) 指定名稱的資料行](columns-with-a-name-specified-as-a-wildcard-character.md)  
  
-   [具有 XPath 節點測試名稱的資料行](columns-with-the-name-of-an-xpath-node-test.md)  
  
-   [以 data&#40;&#41; 指定路徑的資料行名稱](column-names-with-the-path-specified-as-data.md)  
  
-   [預設包含 NULL 值的資料行](columns-that-contain-a-null-value-by-default.md)  
  
-   [PATH 模式中的命名空間支援](namespace-support-in-path-mode.md)  
  
-   [範例：使用 PATH 模式](examples-using-path-mode.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用 WITH XMLNAMESPACES 將命名空間加入至查詢](add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
