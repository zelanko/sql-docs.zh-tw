---
description: 'ICommand (Native Client OLE DB 提供者) '
title: ICommand (Native Client OLE DB 提供者) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f261d8fa00650be277f145c43c13af0ab7c03fa9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483189"
---
# <a name="icommand-native-client-ole-db-provider"></a>ICommand (Native Client OLE DB 提供者) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  本主題討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 特有的 OLE DB 行為。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 插入大於資料行大小的資料通常會產生錯誤。 不過，在一些狀況下會傳回 S_OK，但是會將 *dwStatus* 設定為 DBSTATUS_S_TRUNCATED。 這通常發生于使用參數插入資料時，其中資料行不夠大，無法容納資料，而且尚未呼叫 **ICommandWithParameters：： SetParameterInfo** 。  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](./sql-server-native-client-ole-db-interfaces.md)  
  
