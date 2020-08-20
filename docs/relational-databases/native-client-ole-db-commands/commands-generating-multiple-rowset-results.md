---
description: '產生多個資料列集結果的命令 (Native Client OLE DB 提供者) '
title: 產生多個資料列集結果的命令 (Native Client OLE DB provider) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- SQL Server Native Client OLE DB provider, commands
- SQL Server Native Client OLE DB provider, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
ms.assetid: 4567668d-35fd-4162-b61f-f7536862cdcb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 791ae266a82168239f7c3a9cf99ef90066e8032f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455803"
---
# <a name="sql-server-native-client-commands-generating-multiple-rowset-results"></a>SQL Server Native Client 產生多個資料列集結果的命令
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者可以從語句傳回多個資料列集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式在下列條件下會傳回多個資料列集結果：  
  
-   批次的 SQL 陳述式以單一命令提交。  
  
-   預存程序實作 SQL 陳述式批次。  
  
## <a name="batches"></a>批次  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者會將分號字元辨識為 SQL 語句的批次分隔符號：  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 以一個批次傳送多個 SQL 陳述式，比分開執行每個 SQL 陳述式的效率高。 傳送單一批次可以減少從用戶端到伺服器的網路往返數。  
  
## <a name="stored-procedures"></a>預存程序  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對預存程序中的每個陳述式傳回結果集，所以大部分的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序都會傳回多個結果集。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 IMultipleResults 來處理多個結果集](../../relational-databases/native-client-ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
