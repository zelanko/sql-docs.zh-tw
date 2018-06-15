---
title: 執行命令 |Microsoft 文件
description: 執行命令
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 32bf24bbd652b998e9caaf3e9363445f685c5455
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35304847"
---
# <a name="executing-a-command"></a>執行命令
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  建立資料來源的連接之後，取用者會呼叫 **:: Createsession**方法來建立工作階段。 此工作階段會當做命令、資料列集或交易 Factory 運作。  
  
 若要直接使用個別的資料表或索引，取用者要求**IOpenRowset**介面。 **Iopenrowset:: Openrowset**方法開啟，並傳回包含單一基底資料表或索引的所有資料列的資料列集。  
  
 若要執行命令 (例如 SELECT \* FROM Authors)，取用者要求**IDBCreateCommand**介面。 取用者可以執行**idbcreatecommand:: Createcommand**方法來建立命令物件，並要求**ICommandText**介面。 **Icommandtext:: Setcommandtext**方法用來指定所要執行的命令。  
  
 **Execute**命令用來執行命令。 此命令可以是任何 SQL 陳述式或程序名稱。 並非所有命令都會產生結果集 (資料列集) 物件。 SELECT * FROM Authors 之類的命令會產生結果集。  
  
## <a name="see-also"></a>另請參閱  
 [建立 OLE DB Driver for SQL Server 應用程式](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
