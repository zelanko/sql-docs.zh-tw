---
title: ICommand (OLE DB 驅動程式) | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 的特定 ICommand::Execute 方法的行為。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf787628804f3597fa724c0ab6313a450e365d58
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861905"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  此文章討論 OLE DB Driver for SQL Server 特有的 OLE DB 行為。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 插入大於資料行大小的資料通常會產生錯誤。 但在某些情況下會傳回 S_OK，且 `dwStatus` 會設定為 DBSTATUS_S_TRUNCATED。 這通常發生於以下幾種情況中：

- 插入具有參數的資料時  
- 資料行不夠大而無法保存資料時  
- 未呼叫 `ICommandWithParameters::SetParameterInfo` 時  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
