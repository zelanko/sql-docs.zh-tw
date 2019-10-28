---
title: Multiple Active Result Set (MARS)
description: 描述當 SqlDataReader 的每個實例從個別的命令啟動時，如何在連接上開啟一個以上的 SqlDataReader。
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 7097dc3717966d441cd669ddccd189c2510211aa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452142"
---
# <a name="multiple-active-result-sets-mars"></a>Multiple Active Result Set (MARS)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Multiple Active Result Sets （MARS）是一項功能，允許在單一連接上執行多個批次。 在先前的版本中，一次只能針對單一連接執行一個批次。 使用 MARS 執行多個批次並不表示同時執行作業。  
  
## <a name="in-this-section"></a>本節內容  
[啟用 Multiple Active Result Set](enable-multiple-active-result-sets.md)  
討論如何搭配使用 MARS 與 SQL Server。  
  
[操作資料](manipulate-data.md)  
提供編寫 MARS 應用程式的範例。  
  
## <a name="related-sections"></a>相關章節  
[非同步作業](asynchronous-operations.md)  
提供在 .NET 中使用新異步功能的詳細資料。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
