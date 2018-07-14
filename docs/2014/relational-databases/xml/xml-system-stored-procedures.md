---
title: XML 系統預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7673efc55f780f0ebd99da740c54ea4787b40260
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37215188"
---
# <a name="xml-system-stored-procedures"></a>XML 系統預存程序
  SQL Server 提供以下系統預存程序，可與 OPENXML 一起使用：  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql)  
  
 若要利用 OPENXML 來寫入查詢，您必須先呼叫 **sp_xml_preparedocument**來建立 XML 文件的內部表示。 預存程序將控制代碼傳回 XML 文件的內部表示。 接著將此控制代碼傳遞至 OPENXML。 OPENXML 提供以 XPath 為基礎的文件之資料列集檢視。 具體而言，這是一個資料列模式以及一或多個資料行模式。  
  
> [!NOTE]  
>  由 **sp_xml_preparedocument** 傳回的文件控制代碼在工作階段持續時間內是有效的。  
  
 可呼叫 **sp_xml_removedocument** 系統預存程序來從記憶體中移除 XML 文件的內部表示法。  
  
## <a name="see-also"></a>另請參閱  
 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)   
 [OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md)  
  
  
