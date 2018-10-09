---
title: OLE DB Driver for SQL Server 中的疏鬆資料行支援 | Microsoft Docs
description: OLE DB Driver for SQL Server 中的 UTF-16 支援
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: e0c76b7a62150fe4ee53fd83b63d7b9ebe1fd737
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47641711"
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>在 OLE DB Driver for SQL Server 的 UTF-16 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，如果您在繫結資料行結果或輸出參數時提供固定長度的緩衝區、**wchar** 字元在終止字元成為代理字組的高 Surrogate 字碼指標之前寫入緩衝區，而且下一個 **wchar** 字元是低 Surrogate 字碼指標，OLE DB Driver for SQL Server 就不會將高 Surrogate 字碼指標加入至緩衝區。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
