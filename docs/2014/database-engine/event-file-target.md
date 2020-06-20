---
title: 事件檔案目標 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- event file target
- file target [SQL Server extended events]
- targets [SQL Server extended events], file target
ms.assetid: 4f0ee6ec-a0a8-4c38-aa61-8293ab6ac7fd
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1a64236b3874543982be5abbd8e60d8169082a1e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933058"
---
# <a name="event-file-target"></a>Event File Target
  事件檔案目標是將完整緩衝區寫入磁碟的目標。  
  
 下表說明用來設定事件檔案目標的可用選項。  
  
|選項|允許的值|描述|  
|------------|--------------------|-----------------|  
|filename|最多 260 個字元的任何字串。 這是必要的值。|檔案位置和檔案名稱。<br /><br /> 您可以使用任何副檔名。|  
|max_file_size|任何 64 位元整數。 這是選擇性的值。|最大檔案大小 (以 MB 為單位)。 如果未指定 max_file_size，檔案可以成長到磁碟已滿。 預設的檔案大小為 1GB。<br /><br /> max_file_size 必須大於工作階段緩衝區的目前大小。 如果沒有，檔案目標將無法初始化，而且系統會報告 max_file_size 無效。 若要檢視緩衝區的目前大小，請在 [sys.dm_xe_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql) 動態管理檢視中查詢 buffer_size 資料行。<br /><br /> 如果預設的檔案大小小於工作階段緩衝區大小，我們建議您將 max_file_size 設定為 [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) 目錄檢視中 max_memory 資料行所指定的值。<br /><br /> 當 max_file_size 的大小設定為大於工作階段緩衝區的大小時，它可能會向下捨入到最接近工作階段緩衝區大小的倍數。 這樣做可能會建立小於指定之 max_file_size 值的目標檔案。 例如，如果緩衝區大小是 100MB 而且 max_file_size 設定為 150MB，則產生的檔案就會向下捨入到 100MB，因為其餘 50MB 的空間無法容納第二個緩衝區。<br /><br /> 如果預設的檔案大小小於工作階段緩衝區大小，我們建議您將 max_file_size 設定為 [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) 目錄檢視中 max_memory 資料行的值。|  
|max_rollover_files|任何 32 位元整數。 這是選擇性的值。|要保留在檔案系統中的最大檔案數。 預設值為 5。|  
|increment|任何 32 位元整數。 這是選擇性的值。|檔案的累加成長 (以 MB 為單位)。 如果未指定，increment 的預設值就是工作階段緩衝區大小的兩倍。|  
  
 第一次建立事件檔案目標時，您所指定的檔案名稱會附加 _0\_ 和一個長整數值。 整數值的計算方式為1601年1月1日與建立檔案的日期和時間之間的毫秒數。 後續的換用檔案也會使用這個格式。 透過檢查長整數的值，您就可以判斷出最新的檔案。 下列範例說明您將檔案名稱選項指定為 C:\OutputFiles\MyOutput.xel 的情況下，要如何命名檔案：  
  
-   建立的第一個檔案 - C:\OutputFiles\MyOutput_0_128500310259380000.xel  
  
-   第一個換用檔案 - C:\OutputFiles\MyOutput_0_128505831770890000.xel  
  
-   第二個換用檔案 - C:\OutputFiles\MyOutput_0_132410772966237000.xel  
  
## <a name="adding-the-target-to-a-session"></a>將目標加入至工作階段  
 若要將事件檔案目標加入至擴充事件工作階段，您會在建立或更改事件工作階段時加入下列陳述式，並將 *file_name* 取代成所需的檔案名稱和路徑：  
  
```  
ADD TARGET package0.event_file(  
   SET filename='file_name.xel')  
```  
  
## <a name="reviewing-the-target-output"></a>檢閱目標輸出  
 若要檢閱檔案目標的輸出，您必須使用 sys.fn_xe_file_target_read_file 函數。 我們建議您將資料轉換成 XML。 您可以使用下列語法，並將 *&lt;file_name&gt;* 取代成加入目標時指定的檔案名稱和路徑：  
  
```  
SELECT *, CAST(event_data AS XML) AS 'event_data_XML'  
FROM sys.fn_xe_file_target_read_file('file_name*.xel', NULL, NULL, NULL)  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 擴充事件目標](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [fn_xe_file_target_read_file &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)   
 [&#40;Transact-sql&#41;建立事件會話](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
