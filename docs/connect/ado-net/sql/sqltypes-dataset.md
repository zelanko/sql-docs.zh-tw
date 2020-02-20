---
title: SqlTypes 和資料集
description: 描述資料集中對 SqlTypes 的類型支援。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: a7ef43ca6afa243e313e8e38bdd05d929161e71f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75233785"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes 和資料集

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ADO.NET 2.0 透過 <xref:System.Data.SqlTypes> 命名空間引進了對 `DataSet` 的增強類型支援。 <xref:System.Data.SqlTypes> 中的類型其設計目的是提供與 SQL Server 資料庫中的資料類型具有相同語意及精確度的資料類型。 <xref:System.Data.SqlTypes> 中的每個資料類型，在 SQL Server 中都具有對應的資料類型，並具有相同的基礎資料表示。  
  
直接在 <xref:System.Data.DataSet> 中使用 <xref:System.Data.SqlTypes>，會在使用 SQL Server 資料類型時帶來數個優點。 <xref:System.Data.SqlTypes> 支援與 SQL Server 原生資料類型相同的語意。 在 <xref:System.Data.DataColumn> 的定義中指定其中一個 <xref:System.Data.SqlTypes>，在將十進位或數值資料類型轉換為通用語言執行平台 (CLR) 資料類型之一時就不會發生精確度遺失。  

下列範例建立 <xref:System.Data.DataTable> 物件，其會使用 <xref:System.Data.SqlTypes> 而非 CLR 類型，來明確定義 <xref:System.Data.DataColumn> 資料類型。 該程式碼會將 SQL Server 中 AdventureWorks 資料庫內 Sales.SalesOrderDetail 資料表的資料，填入 <xref:System.Data.DataTable>。 主控台視窗中顯示的輸出會顯示每個資料行的資料類型，以及擷取自 SQL Server 的值。  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
