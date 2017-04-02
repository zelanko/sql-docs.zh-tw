---
title: "使用者自訂資料類型 (UDT) 的 FOR XML 支援 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UDT [SQL Server], XML"
  - "使用者定義類型 [SQL Server], XML"
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 使用者自訂資料類型 (UDT) 的 FOR XML 支援
  FOR XML 不支援 Common Language Runtime (CLR) 使用者定義資料類型 (UDT)。  
  
 若要搭配 CLR 使用者定義資料類型使用 FOR XML，請確定此資料類型有 XML 序列化，並在 FOR XML SELECT 子句中使用 XML 的明確轉換。  
  
## 另請參閱  
 [各個 SQL Server 資料類型的 FOR XML 支援](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  