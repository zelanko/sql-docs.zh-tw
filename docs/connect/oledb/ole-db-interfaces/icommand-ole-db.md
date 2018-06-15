---
title: ICommand (OLE DB) |Microsoft 文件
description: ICommand 介面 (OLE DB)
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
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3f8599e9e353b4683b59e5717e25812b8562aed8
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35305997"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  這篇文章討論 OLE DB 驅動程式的特定 SQL Server 的 OLE DB 行為。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 插入大於資料行大小的資料通常會產生錯誤。 不過，有很多情況下會傳回 S_OK，但*dwStatus*會設定為 DBSTATUS_S_TRUNCATED。 它通常會發生使用參數插入資料時，資料行不是夠大，無法保存資料，以及**icommandwithparameters:: Setparameterinfo**尚未被呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
