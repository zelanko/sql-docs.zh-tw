---
title: "sysmergeschemachange (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergeschemachange_TSQL
- sysmergeschemachange
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemachange system table
ms.assetid: ae9ce16e-6ee9-4c7c-8210-a9bf2c7efdf0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f42fbeba8639216d5a95414430099fbd5bde0b07
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergeschemachange-transact-sql"></a>sysmergeschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含快照集代理程式所產生之已發行的發行項之相關資訊。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**pubid**|**uniqueidentifier**|發行集的識別碼。|  
|**artid**|**uniqueidentifier**|發行項的識別碼。|  
|**schemaversion**|**int**|前一個結構描述變更的編號。|  
|**schemaguid**|**uniqueidentifier**|前一個結構描述的唯一識別碼。|  
|**schematype**|**int**|結構描述變更的類型：<br /><br /> **-1** = 無效。<br /><br /> **1** = SQL 命令。<br /><br /> **2** = 結構描述指令碼。<br /><br /> **3** = 原生大量複製程式公用程式 (BCP)。<br /><br /> **4** = 字元 BCP。<br /><br /> **5** = 最後一個記錄產生。<br /><br /> **6** = 上次傳送的生成集。<br /><br /> **7** = 目錄。<br /><br /> **8** = 優先順序。<br /><br /> **9** = 保留期限。<br /><br /> **10** = 觸發程序的指令碼。<br /><br /> **11** = 變更資料表。<br /><br /> **12** = 全部重新初始化。<br /><br /> **13** = 變更資料表 (非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。<br /><br /> **14** = 以上傳重新初始化。<br /><br /> **15** = 條件約束和索引的指令碼。<br /><br /> **16** = 清除中繼資料。<br /><br /> **17** = 更新上次傳送的生成集。<br /><br /> **18** = 回溯相容性層級。<br /><br /> **19** = 驗證訂閱者資訊。<br /><br /> **20** = 已妥善分割。<br /><br /> **21** = 自訂解析程式。<br /><br /> **22** = 發行項處理順序。<br /><br /> **23** = 交易式發行集中發行。<br /><br /> **24** = 彌補錯誤。<br /><br /> **25** = 替代快照集資料夾。<br /><br /> **26** = 僅限下載。<br /><br /> **27** = 刪除追蹤。<br /><br /> **40** = 預先建立快照集指令碼。<br /><br /> **45** = 後續建立快照集指令碼。<br /><br /> **46** = 視使用者指令碼。<br /><br /> **50** = 快照集標頭開始。<br /><br /> **51** = 快照集標頭結束。<br /><br /> **52** = 快照集結尾。<br /><br /> **53** = 檔案傳輸通訊協定 (FTP) 位址。<br /><br /> **54** = FTP 通訊埠。<br /><br /> **55** = FTP 子目錄。<br /><br /> **56** = 壓縮快照集。<br /><br /> **57** = FTP 登入。<br /><br /> **58** = FTP 密碼。<br /><br /> **60** = 系統預先建立指令碼。<br /><br /> **61** = 預存程序結構描述。<br /><br /> **62** = 檢視結構描述。<br /><br /> **63** = 使用者定義函數的結構描述。<br /><br /> **64** = 檢視索引。<br /><br /> **65** = 擴充屬性。<br /><br /> **66** = 驗證。<br /><br /> **67** = 前快照集的 SQL 命令。<br /><br /> **71** = 動態快照集驗證。<br /><br /> **80** = 系統資料表原生 BCP 9.0。<br /><br /> **81** = 系統資料表字元 BCP 9.0。<br /><br /> **82** = 系統資料表原生 BCP 9.0 （僅限全域）。<br /><br /> **83** = 系統資料表字元 BCP 9.0 （僅限全域）。<br /><br /> **84** = 系統資料表原生 BCP 9.0 （輕量型）。<br /><br /> **85** = 系統資料表字元 BCP 9.0 （輕量型）。<br /><br /> **128** = 動態 BCP （位元）。<br /><br /> **131** = 動態原生 BCP。<br /><br /> **132** = 動態字元 BCP。<br /><br /> **208** = 動態系統資料表原生 BCP 9.0。<br /><br /> **209** = 動態系統資料表字元 BCP 9.0。<br /><br /> **210** = 動態系統資料表原生 BCP 9.0 （僅限全域）。<br /><br /> **211** = 動態系統資料表字元 BCP 9.0 （僅限全域）。<br /><br /> **212** = 動態系統資料表原生 BCP 9.0 （輕量型）。<br /><br /> **213** = 動態系統資料表字元 BCP 9.0 （輕量型）。<br /><br /> **300** = 資料定義語言 (DDL) 動作。<br /><br /> **1024** = 累加快照集的控制項。<br /><br /> **1049** = 累加快照集資料夾。<br /><br /> **1074** = 累加快照集開始標頭。<br /><br /> **1075** = 累加快照集結束標頭。<br /><br /> **1076** = 累加快照集結尾。<br /><br /> **1077** = 累加 FTP 位址。<br /><br /> **1078** = 累加 FTP 通訊埠。<br /><br /> **1079** = 累加 FTP 子目錄。<br /><br /> **1080** = 累加壓縮快照集。<br /><br /> **1081** = 累加 FTP 登入。<br /><br /> **1082** = 累加 FTP 密碼。|  
|**schematext**|**nvarchar(2000)**|指令碼檔案的名稱，或是包含檔案名稱的命令|  
|**schemastatus**|**tinyint**|指出發行項的結構描述變更是否暫止，它可以是下列值之一：<br /><br /> **0** = 非使用中。<br /><br /> **1** = 使用。<br /><br /> 暫止結構描述變更時，此值設定為**1**。|  
|**schemasubtype**|**int**|結構描述變更的子類型：<br /><br /> **1** = ADDCOLUMN<br /><br /> **2** = DROPCOLUMN<br /><br /> **3** = ALTERCOLUMN<br /><br /> **4** = ADDPRIMARYKEY<br /><br /> **5** = ADDUNIQUE<br /><br /> **6** = ADDREFERENCE<br /><br /> **7** = DROPCONSTRAINT<br /><br /> **8** = ADDDEFAULT<br /><br /> **9** = ADDCHECK<br /><br /> **10** = DISABLETRIGGER<br /><br /> **11** = ENABLETRIGGER<br /><br /> **12** = DISABLETRIGGER<br /><br /> **13** = ENABLETRIGGER<br /><br /> **14** = ENABLECONSTRAINT<br /><br /> **15** = DISABLECONSTRAINT<br /><br /> **16** = ENABLECONSTRAINT<br /><br /> **17** = DISABLECONSTRAINT|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
