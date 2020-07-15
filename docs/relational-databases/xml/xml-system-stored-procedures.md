---
title: XML 系統預存程序 | Microsoft Docs
description: 了解由 SQL Server 所提供用來撰寫 OPENXML 查詢的 XML 系統預存程序。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e3b6a8e61befce3dd68bd692976b25d0d9d7259
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729762"
---
# <a name="xml-system-stored-procedures"></a>XML 系統預存程序
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  SQL Server 提供以下系統預存程序，可與 OPENXML 一起使用：  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)  
  
 若要利用 OPENXML 來寫入查詢，您必須先呼叫 **sp_xml_preparedocument**來建立 XML 文件的內部表示。 預存程序將控制代碼傳回 XML 文件的內部表示。 接著將此控制代碼傳遞至 OPENXML。 OPENXML 提供以 XPath 為基礎的文件之資料列集檢視。 具體而言，這是一個資料列模式以及一或多個資料行模式。  
  
> [!NOTE]  
>  由 **sp_xml_preparedocument** 傳回的文件控制代碼在工作階段持續時間內是有效的。  
  
 可呼叫 **sp_xml_removedocument** 系統預存程序來從記憶體中移除 XML 文件的內部表示法。  
  
## <a name="see-also"></a>另請參閱  
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
