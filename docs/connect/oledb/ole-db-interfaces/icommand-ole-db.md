---
title: ICommand (OLE DB) |Microsoft Docs
description: ICommand 介面 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 9622dfa505fd00bca639d1cfd8919aef4145a85a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790670"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  這篇文章討論特定 OLE DB Driver for SQL Server 的 OLE DB 行為。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 插入大於資料行大小的資料通常會產生錯誤。 不過，在一些狀況下會傳回 S_OK，但是會將 *dwStatus* 設定為 DBSTATUS_S_TRUNCATED。 它通常會發生使用參數插入資料時，資料行不是夠大，無法保存資料，並**icommandwithparameters:: Setparameterinfo**尚未被呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
