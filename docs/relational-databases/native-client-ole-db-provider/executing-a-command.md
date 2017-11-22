---
title: "執行命令 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-provider
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e37688d49155aa0d3735e1be332e41b0ae79447
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="executing-a-command"></a>執行命令
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  建立資料來源的連接之後，取用者會呼叫**:: Createsession**方法來建立工作階段。 此工作階段會當做命令、資料列集或交易 Factory 運作。  
  
 若要直接使用個別的資料表或索引，取用者要求**IOpenRowset**介面。 **Iopenrowset:: Openrowset**方法開啟，並傳回包含單一基底資料表或索引的所有資料列的資料列集。  
  
 若要執行命令 (例如 SELECT \* FROM Authors)，取用者要求**IDBCreateCommand**介面。 取用者可以執行**idbcreatecommand:: Createcommand**方法來建立命令物件，並要求**ICommandText**介面。 **Icommandtext:: Setcommandtext**方法用來指定所要執行的命令。  
  
 **Execute**命令用來執行命令。 此命令可以是任何 SQL 陳述式或程序名稱。 並非所有命令都會產生結果集 (資料列集) 物件。 SELECT * FROM Authors 之類的命令會產生結果集。  
  
## <a name="see-also"></a>請參閱＜  
 [建立 SQL Server Native Client OLE DB 提供者應用程式](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
