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
ms.openlocfilehash: 3ca08ca3439c2dde50cb4a7a1226688854fd6fe0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994966"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>在 OLE DB Driver for SQL Server 中使用具有 OLE DB 的 OUTPUT 子句
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  如果您在 INSERT、UPDATE、DELETE 或 MERGE 命令中使用 OUTPUT 子句，受影響的資料列計數就無法使用。 應用程式必須計算 OUTPUT 子句所傳回的資料列集中的資料列數。  
  
## <a name="see-also"></a>另請參閱  
 [建立 OLE DB Driver for SQL Server 應用程式](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
