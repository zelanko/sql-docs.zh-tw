---
title: SqlTypes 和資料集
description: 描述資料集中 SqlTypes 的類型支援。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 70efb8615a70677c709abd6d9129c63de9420ffc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451979"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes 和資料集

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ADO.NET 2.0 透過 <xref:System.Data.SqlTypes> 命名空間引進了 `DataSet` 的增強型別支援。 <xref:System.Data.SqlTypes> 中的類型其設計目的是提供與 SQL Server 資料庫中的資料類型具有相同語意及精確度的資料類型。 <xref:System.Data.SqlTypes> 中的每個資料類型，在 SQL Server 中都具有對應的資料類型，並具有相同的基礎資料表示。  
  
直接在 <xref:System.Data.DataSet> 中使用 <xref:System.Data.SqlTypes>，會在使用 SQL Server 資料類型時授數個優點。 <xref:System.Data.SqlTypes> 支援與 SQL Server 原生資料類型相同的語義。 在 <xref:System.Data.DataColumn> 的定義中指定其中一個 <xref:System.Data.SqlTypes>，可排除將 decimal 或 numeric 資料類型轉換成其中一個 common language runtime （CLR）資料類型時，可能發生的精確度遺失。  

下列範例建立 <xref:System.Data.DataTable> 物件，其會使用 <xref:System.Data.SqlTypes> 而非 CLR 類型，來明確定義 <xref:System.Data.DataColumn> 資料類型。 該程式碼會將 SQL Server 中 AdventureWorks 資料庫內 Sales.SalesOrderDetail 資料表的資料，填入 <xref:System.Data.DataTable>。 主控台視窗中顯示的輸出會顯示每個資料行的資料類型，以及從 SQL Server 取出的值。  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
