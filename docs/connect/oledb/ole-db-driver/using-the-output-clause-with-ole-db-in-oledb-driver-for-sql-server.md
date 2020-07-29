---
title: 在 OLE DB Driver for SQL Server 中使用具有 OLE DB 的 OUTPUT 子句 | Microsoft Docs
description: 在 OLE DB Driver for SQL Server 中使用具有 OLE DB 的 OUTPUT 子句
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: df9868d5cd5c7a47c88891abe6b837c68edc784b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003385"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>在 OLE DB Driver for SQL Server 中使用具有 OLE DB 的 OUTPUT 子句
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  如果您在 INSERT、UPDATE、DELETE 或 MERGE 命令中使用 OUTPUT 子句，受影響的資料列計數就無法使用。 應用程式必須計算 OUTPUT 子句所傳回的資料列集中的資料列數。  
  
## <a name="see-also"></a>另請參閱  
 [建立 OLE DB Driver for SQL Server 應用程式](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
