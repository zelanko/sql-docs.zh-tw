---
title: 架構的用戶端和伺服器端 XML 格式化 (SQLXML 4.0) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], XML formatting architecture
- SQLOLEDB provider
- client-side XML formatting
- data providers [SQLXML], XML formatting architecture
- SQLNCLI, XML
- server-side XML formatting
- SQL Server Native Client, XML
- SQLXMLOLEDB Provider, XML formatting architecture
ms.assetid: 52440d9e-89fd-4c15-a008-a1ea99f41387
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 32fd7cf959e5dbf87b0052e32f796428ede3f040
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="architecture-of-client-side-and-server-side-xml-formatting-sqlxml-40"></a>用戶端和伺服器端 XML 格式的架構 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  下圖顯示伺服器端上的 XML 格式的架構。  
  
 ![伺服器端 XML 格式化架構。](../../../relational-databases/sqlxml/formatting/media/serversidexml.gif "伺服器端格式架構的 XML。")  
  
 在此範例中，在用戶端上指定的命令會傳送至伺服器。 伺服器會產生 XML 文件，然後再將文件傳回給用戶端。 在此情況下，伺服器會有的執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 在使用伺服器端 XML 格式時，您可以使用 SQLXMLOLEDB 提供者或 SQLOLEDB 提供者。  SQLXMLOLEDB 提供者會使用 Sqlxml4.dll，此檔案包含在 SQLXML 4.0 中。 當您使用 SQLOLEDB 提供者時，根據預設，您會取得由 Sqlxmlx.dll 提供的 SQLXML 功能，Sqlxmlx.dll 是包含在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 或者 Microsoft Data Access Components (MDAC) 2.6 或更新版本中。 若要搭配 SQLOLEDB 使用 Sqlxml4.dll，您必須在 SQLOLEDB 連線物件上設定 SQLXML Version 屬性為"SQLXML.4.0"。 不論是何種情況，伺服器都會產生 XML 文件，然後再將文件傳回給用戶端。  
  
> [!NOTE]  
>  XPath 查詢和 Updategram 會在用戶端上進行剖析。 若要取得 SQLXML 4.0 中的 XPath 範本或 Updategram 功能，請使用 Sqlxml4.dll。  
  
 下圖顯示用戶端端上的 XML 格式的架構。  
  
 ![在用戶端 XML 格式化架構。](../../../relational-databases/sqlxml/formatting/media/clientsidexml.gif "架構的 XML 格式化的用戶端。")  
  
 在這個範例中，用戶端會使用 SQLXMLOLEDB 提供者。 在連接字串必須為 SQLOLEDB 設定資料提供者屬性。 (這是 SQLXML 4.0 中唯一接受的值)。在用戶端上執行的命令會傳送至伺服器。 在伺服器上產生的資料列集會傳送至用戶端。 來自資料列集的 XML 文件的格式會在用戶端上執行。  
  
 在 SQLXML 4.0 中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) 或 SQLOLEDB 提供者可用來當做資料提供者。 您可能可以存取任何資料來源。 只要查詢傳回單一資料列集，就可以在用戶端上套用 XML 轉換。  
  
  
