---
title: SQL Server 的 OLE DB 驅動程式中的 utf-16 支援 |Microsoft 文件
description: SQL Server 的 OLE DB 驅動程式中的 utf-16 支援
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0f710e6f567f789771a80677beb24d24b1c8f5d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>SQL Server 的 OLE DB 驅動程式中的 utf-16 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  從開始[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，如果您在繫結資料行結果或輸出參數時提供固定長度的緩衝區，而且如果**wchar**結束的字元為高 surrogate 字碼指標之前寫入緩衝區的字元surrogate 字組，而且如果下一個**wchar**字元是低 surrogate 字碼指標、 OLE DB 驅動程式的 SQL Server 不會將高 surrogate 字碼指標加入至緩衝區。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
