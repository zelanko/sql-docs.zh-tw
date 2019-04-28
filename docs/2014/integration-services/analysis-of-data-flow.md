---
title: 資料流程分析 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 5654cb30-cad2-470c-97b3-59cb331033e5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 154778d2c3a4056e1b16743ff629e4c4a5dae0a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62836566"
---
# <a name="analysis-of-data-flow"></a>資料流程分析
  您可以使用[catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) `SSISDB`資料庫檢視，分析封裝的資料流程。 每當資料流程元件傳送資料至下游元件，此檢視就會顯示一個資料列。 您可以使用這項資訊深入了解傳送至每個元件的資料列。  
  
> [!NOTE]  
>  您必須將記錄層次設定為 [詳細資訊]，以透過 catalog.execution_data_statistics 檢視來擷取資訊。  
  
 下列範例顯示在封裝元件之間傳送的資料列數。  
  
```  
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name  
  
```  
  
 下列範例計算針對特定執行，每個元件每毫秒所傳送的資料列數目。 計算值包括：  
  
-   **total_rows** - 元件傳送的所有資料列總和  
  
-   **wall_clock_time_ms** - 每個元件經過的執行時間總計 (以毫秒為單位)  
  
-   **num_rows_per_millisecond** - 每個元件每毫秒傳送的資料列數  
  
 `HAVING`子句用來防止在計算中的除以零錯誤。  
  
```  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
  
```  
  
## <a name="related-tasks"></a>相關工作  
 [偵錯資料流程](troubleshooting/debugging-data-flow.md)  
  
 [套件執行的疑難排解工具](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料流程中的資料](data-flow/data-in-data-flows.md)  
  
  
