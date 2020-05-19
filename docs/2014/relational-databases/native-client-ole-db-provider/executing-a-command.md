---
title: 執行命令 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 47307455468a20351c3a3cda2a619e6296fb29ad
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704727"
---
# <a name="executing-a-command"></a>執行命令
  建立資料來源的連接後，取用者會呼叫 **IDBCreateSession::CreateSession** 方法來建立工作階段。 此工作階段會當做命令、資料列集或交易 Factory 運作。  
  
 若要直接使用個別的資料表或索引，取用者會要求 `IOpenRowset` 介面。 `IOpenRowset::OpenRowset` 方法會從單一基底資料表或索引開啟並傳回包含所有資料列的資料列集。  
  
 若要執行命令（例如 SELECT \* FROM 作者），取用者會要求 `IDBCreateCommand` 介面。 取用者可以執行 `IDBCreateCommand::CreateCommand` 方法來建立命令物件並要求 `ICommandText` 介面。 `ICommandText::SetCommandText` 方法用於指定即將執行的命令。  
  
 `Execute` 命令用於執行命令。 此命令可以是任何 SQL 陳述式或程序名稱。 並非所有命令都會產生結果集 (資料列集) 物件。 SELECT * FROM Authors 之類的命令會產生結果集。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SQL Server Native Client OLE DB 提供者應用程式](creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
