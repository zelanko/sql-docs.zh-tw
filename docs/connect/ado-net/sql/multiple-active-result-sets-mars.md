---
title: Multiple Active Result Set (MARS)
description: 描述從個別命令啟動 SqlDataReader 的每個執行個體時，如何在連線上開啟一個以上的 SqlDataReader。
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: e93493a28adfecd7dd39c79a86170b06ed18b992
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924284"
---
# <a name="multiple-active-result-sets-mars"></a>Multiple Active Result Set (MARS)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Multiple Active Result Set (MARS) 是可允許在單一連線中執行多個批次作業的功能。 在先前版本中，針對單一連線，一次只能執行一個批次。 使用 MARS 執行多個批次，並非意味著同時執行作業。  
  
## <a name="in-this-section"></a>本節內容  
[啟用 Multiple Active Result Set](enable-multiple-active-result-sets.md)  
討論如何搭配使用 MARS 與 SQL Server。  
  
[操作資料](manipulate-data.md)  
提供撰寫 MARS 應用程式程式碼的範例。  
  
## <a name="related-sections"></a>相關章節  
[非同步作業](asynchronous-operations.md)  
提供在 .NET 中使用新的非同步功能的詳細資料。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
