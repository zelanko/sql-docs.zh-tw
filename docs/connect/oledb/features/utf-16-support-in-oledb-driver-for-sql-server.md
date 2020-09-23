---
title: OLE DB Driver for SQL Server 中的 UTF-16 支援 | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 中的 UTF-16 支援，以及其新增高 Surrogate 字碼元素至緩衝區的時機。
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f00b9f0ac10c812743cac0bf4222fd2136710b42
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861786"
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 中的 UTF-16 支援
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，如果您在繫結資料行結果或輸出參數時提供固定長度的緩衝區、**wchar** 字元在終止字元成為代理字組的高 Surrogate 字碼指標之前寫入緩衝區，而且下一個 **wchar** 字元是低 Surrogate 字碼指標，OLE DB Driver for SQL Server 就不會將高 Surrogate 字碼指標加入至緩衝區。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
