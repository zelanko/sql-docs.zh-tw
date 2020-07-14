---
title: 使用 XSINIL 為 NULL 值產生元素 | Microsoft Docs
description: 了解如何透過在 ELEMENTS 指示詞上使用 XSINIL 參數來針對 NULL 值產生 XML 元素。
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 7cf18eb7c5dea9a61988533205a3a64ab1ae3fd0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85638947"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>使用 XSINIL 參數為 NULL 值產生元素

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**ELEMENTS** 指示詞可建構 XML，在其中每個資料行值都對應到 XML 中的元素。 根據預設，若資料行值為 NULL，便不會新增任何項目。 但是，若在 ELEMENTS 指示詞上指定選擇性的 **XSINIL** 參數，您可以要求也為 NULL 值建立項目。 在此情況下，對於每個 NULL 資料行值，會傳回一個 **xsi:nil** 屬性設定成 TRUE 的元素。  
  
## <a name="see-also"></a>另請參閱

[搭配 FOR XML 使用 RAW 模式](../../relational-databases/xml/use-raw-mode-with-for-xml.md)

[SELECT - FOR 子句](../../t-sql/queries/select-for-clause-transact-sql.md)
