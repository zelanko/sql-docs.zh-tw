---
title: "系統基底資料表 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- system base tables [SQL Server]
- hobt [SQL Server]
- base tables
ms.assetid: 31f2df90-651f-4699-8067-19f59b60904f
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 80200caa85c27f1568b02c573b51ec0bd1a7b0f1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="system-base-tables"></a>系統基底資料表
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  系統基底資料表其實是儲存特定資料庫之中繼資料的基礎資料表。 **主要**資料庫是特殊在這一方面，因為它包含的任何其他資料庫中找不到某些其他資料表。 這些資料表包含整個伺服器範圍所保存的中繼資料。  
  
> [!IMPORTANT]  
>  系統基底資料表僅用於 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 內部，不供一般客戶使用。 它們隨時可以變更，而且不保證其相容性。  
  
## <a name="system-base-table-metadata"></a>系統基底資料表中繼資料  
 在資料庫上具有 CONTROL、 ALTER 或 VIEW DEFINITION 權限授與者可以看到系統基底資料表的中繼資料中**sys.objects**目錄檢視。 被授與者也可以解析名稱，並且使用內建函數，例如物件的系統基底資料表的識別碼[OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md)和[OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)。  
  
 若要繫結至系統基底資料表，使用者必須使用專用管理員連接 (DAC)，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 嘗試在不使用 DAC 連接的情況下，從系統基底資料表執行 SELECT 查詢時，會產生錯誤。  
  
> [!IMPORTANT]  
>  使用 DAC 存取系統基底資料表的設計僅適用於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 人員，因此這不是受支援的客戶案例。  
  
## <a name="system-base-tables"></a>系統基底資料表  
 下表列出並描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的每個系統基底資料表。  
  
|基底資料表|Description|  
|----------------|-----------------|  
|**sys.sysschobjs**|存在於每個資料庫中。 每一個資料列都代表資料庫中的一個物件。|  
|**sys.sysbinobjs**|存在於每個資料庫中。 資料庫中的每個 Service Broker 實體都包含一個資料列。 Service Broker 實體包括下列各項：<br /><br /> 訊息類型<br /><br /> 服務合約<br /><br /> 服務<br /><br /> 名稱和類型會使用修復過的二進位定序。|  
|**sys.sysclsobjs**|存在於每個資料庫中。 每個分類的實體都包含一個資料列，該實體會共用相同的通用屬性，包括：<br /><br /> 組件<br /><br /> 備份裝置<br /><br /> 全文檢索目錄<br /><br /> 分割區函數<br /><br /> 分割區配置<br /><br /> 檔案群組<br /><br /> 模糊化索引鍵|  
|**sys.sysnsobjs**|存在於每個資料庫中。 每個命名空間範圍的實體都包含一個資料列。 此資料表用於儲存 XML 集合實體。|  
|**sys.syscolpars**|存在於每個資料庫中。 資料表、檢視或資料表值函數中的每個資料行都包含一個資料列。 對於程序或函數的每個參數，它也包含資料列。|  
|**sys.systypedsubobjs**|存在於每個資料庫中。 每個輸入的子實體都包含一個資料列。 只有資料分割函數的參數屬於這個類別目錄。|  
|**sys.sysidxstats**|存在於每個資料庫中。 針對資料表和索引檢視的每個索引或統計資料，各包含一個資料列。<br /><br /> 注意： 每個索引 （堆積除外） 是與具有相同名稱做為索引的統計資料相關聯。|  
|**sys.sysiscols**|存在於每個資料庫中。 每個保存的索引和統計資料資料行都包含一個資料列。|  
|**sys.sysscalartypes**|存在於每個資料庫中。 每個使用者自訂或系統類型都包含一個資料列。|  
|**sys.sysdbreg**|存在於**主要**只有資料庫。 每個註冊的資料庫都包含一個資料列。|  
|**sys.sysxsrvs**|存在於**主要**只有資料庫。 每個本機、連結或遠端伺服器都包含一個資料列。|  
|**sys.sysrmtlgns**|此系統基底資料表存在於**主要**只有資料庫。 每個遠端登入對應都包含一個資料列。 這用來將宣告為來自對應伺服器的內送登入對應至實際的本機登入。|  
|**sys.syslnklgns**|存在於**主要**只有資料庫。 每個連結登入對應都包含一個資料列。 連結登入對應是由從遠端伺服器發出到對應連結伺服器的遠端程序呼叫和分散式查詢所使用。|  
|**sys.sysxlgns**|存在於**主要**只有資料庫。 每個伺服器主體都包含一個資料列。|  
|**sys.sysdbfiles**|存在於每個資料庫中。 如果資料行**dbid**為零，資料列代表屬於此資料庫的檔案。 在**主要**資料庫、 資料行**dbid**可以是非零。 如果是這個情況，資料列代表主檔案。|  
|**sys.sysusermsg**|存在於**主要**只有資料庫。 每個資料列都代表一個使用者自訂的錯誤訊息。|  
|**sys.sysprivs**|存在於每個資料庫中。 每個資料庫或伺服器層級的權限都包含一個資料列。<br /><br /> 附註： 伺服器層級權限儲存在**主要**資料庫。|  
|**sys.sysowners**|存在於每個資料庫中。 每個資料列都代表一個資料庫主體。|  
|**sys.sysobjkeycrypts**|存在於每個資料庫中。 與物間相關聯的每個對稱金鑰、加密或密碼編譯屬性都包含一個資料列。|  
|**sys.syscerts**|存在於每個資料庫中。 資料庫中的每個憑證都包含一個資料列。|  
|**sys.sysasymkeys**|存在於每個資料庫中。 每個資料列都代表一個非對稱金鑰。|  
|**sys.ftinds**|存在於每個資料庫中。 資料庫中的每個全文檢索索引都包含一個資料列。|  
|**sys.sysxprops**|存在於每個資料庫中。 每個擴充屬性都包含一個資料列。|  
|**sys.sysallocunits**|存在於每個資料庫中。 每個儲存配置單位都包含一個資料列。|  
|**sys.sysrowsets**|存在於每個資料庫中。 索引或堆積的每個資料分割資料列集都包含一個資料列。|  
|**sys.sysrowsetrefs**|存在於每個資料庫中。 資料列集參考的每個索引都包含一個資料列。|  
|**sys.syslogshippers**|存在於**主要**只有資料庫。 針對每個資料庫鏡像見證都包含一個資料列。|  
|**sys.sysremsvcbinds**|存在於每個資料庫中。 每個遠端服務繫結都包含一個資料列。|  
|**sys.sysconvgroup**|存在於每個資料庫中。 Service Broker 中的每個服務執行個體都包含一個資料列。|  
|**sys.sysxmitqueue**|存在於每個資料庫中。 每個 Service Broker 傳輸佇列都包含一個資料列。|  
|**sys.sysdesend**|存在於每個資料庫中。 Service Broker 轉換的每個傳送端點都包含一個資料列。|  
|**sys.sysdercv**|存在於每個資料庫中。 Service Broker 轉換的每個接收端點都包含一個資料列。|  
|**sys.sysendpts**|存在於**主要**只有資料庫。 在伺服器中建立的每個端點都包含一個資料列。|  
|**sys.syswebmethods**|存在於**主要**只有資料庫。 在 SOAP 之 HTTP 端點 (在伺服器中建立的) 上定義的每個 SOAP 方法都包含一個資料列。|  
|**sys.sysqnames**|存在於每個資料庫中。 每個命名空間或符合 4 位元組識別碼語彙基元的名稱都包含一個資料列。|  
|**sys.sysxmlcomponent**|存在於每個資料庫中。 每個資料列都代表一個 XML 結構描述元件。|  
|**sys.sysxmlfacet**|存在於每個資料庫中。 XML 類型定義的每個 XML Facet (限制) 都包含一個資料列。|  
|**sys.sysxmlplacement**|存在於每個資料庫中。 XML 元件的每個 XML 位置都包含一個資料列。|  
|**sys.syssingleobjrefs**|存在於每個資料庫中。 每個一般 N 對 1 參考都包含一個資料列。|  
|**sys.sysmultiobjrefs**|存在於每個資料庫中。 每個一般 N 對 N 參考都包含一個資料列。|  
|**sys.sysobjvalues**|存在於每個資料庫中。 實體的每個一般值屬性都包含一個資料列。|  
|**sys.sysguidrefs**|存在於每個資料庫中。 每個 GUID 分類的識別碼參考都包含一個資料列。|  
  
  
