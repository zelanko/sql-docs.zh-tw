---
title: "資料流程分析 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5654cb30-cad2-470c-97b3-59cb331033e5
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# 資料流程分析
  您可以使用 [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) **SSISDB** 資料庫檢視，分析封裝的資料流程。 每當資料流程元件傳送資料至下游元件，此檢視就會顯示一個資料列。 您可以使用這項資訊深入了解傳送至每個元件的資料列。  
  
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
  
-   **wall_clock_time_ms** – 每個元件經過的執行時間總計 (以毫秒為單位)  
  
-   **num_rows_per_millisecond** – 每個元件每毫秒傳送的資料列數  
  
 **HAVING** 子句可用來避免在計算中發生除以零的錯誤。  
  
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
  
## 相關工作  
 [偵錯資料流程](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
## 請參閱＜  
 [資料流程中的資料](../../integration-services/data-flow/data-in-data-flows.md)  
  
  