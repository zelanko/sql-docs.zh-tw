---
title: SQL Server Express LocalDB 執行個體 API 參考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: faec46da-0536-4de3-96f3-83e607c8a8b6
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 211e7a076cae09b3fef7ef40a23cca9c60910e47
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37154301"
---
# <a name="sql-server-express-localdb-instance-api-reference"></a>SQL Server Express LocalDB 執行個體 API 參考
  在傳統、服務架構的 SQL Server 環境中，安裝在單一電腦上的個別 SQL Server 執行個體實體上是分隔的；亦即，每個執行個體必須個別予以安裝及移除、具有獨立的一組二進位檔，以及在個別的服務處理序下執行。 SQL Server 執行個體名稱可用來指定使用者想要連接的 SQL Server 執行個體。  
  
 SQL Server Express LocalDB 執行個體 API 會使用經過簡化的「輕量型」執行個體模型。 雖然個別 LocalDB 執行個體會在不同的磁碟和登錄中，但是會使用同一組共用的 LocalDB 二進位檔。 此外，LocalDB 不會使用服務；LocalDB 執行個體會視需要透過 LocalDB 執行個體 API 呼叫來啟動。 在 LocalDB 中，執行個體名稱可用來指定使用者想要使用的 LocalDB 執行個體。  
  
 除非啟用執行個體共用，否則每個 LocalDB 執行個體一律只能由一位使用者所擁有，且只能透過此使用者的內容進行檢視及存取。  
  
 雖然 LocalDB 執行個體在技術上與傳統的 SQL Server 執行個體不同，但是其用途很類似。 在呼叫*執行個體*來強調這項相似性，並讓 SQL Server 使用者更具直覺性。  
  
 LocalDB 支援兩種執行個體：自動執行個體 (AI) 和具名執行個體 (NI)。 LocalDB 執行個體的識別碼是執行個體名稱。  
  
## <a name="automatic-localdb-instances"></a>自動 LocalDB 執行個體  
 自動 LocalDB 執行個體為「公用」；這些執行個體會自動為使用者建立及管理，並且可供任何應用程式使用。 使用者電腦上安裝的每一個 LocalDB 版本各存在一個自動 LocalDB 執行個體。  
  
 自動 LocalDB 執行個體提供順暢的執行個體管理。 使用者不需要建立執行個體。 這讓使用者可以輕鬆安裝應用程式，並移轉至不同的電腦。 如果目標電腦已安裝指定的 LocalDB 版本，該電腦也可以使用此版本的自動 LocalDB 執行個體。  
  
### <a name="automatic-instance-management"></a>自動執行個體管理  
 使用者不需要建立自動 LocalDB 執行個體。 如果使用者電腦可以使用指定的 LocalDB 版本，第一次使用執行個體時會以延遲的方式來建立執行個體。 從使用者的觀點來看，如果存在 LocalDB 二進位檔，則一律存在自動執行個體。  
  
 刪除、共用及取消共用等其他執行個體管理作業也適用於自動執行個體。 具體而言，刪除自動執行個體會有效地重設執行個體，進而在下一個啟動作業中重新建立。 如果系統資料庫損毀，可能需要刪除自動執行個體。  
  
### <a name="automatic-instance-naming-rules"></a>自動執行個體命名規則  
 自動 LocalDB 執行個體的執行個體名稱採用屬於保留命名空間的特殊模式。 為了避免與具名 LocalDB 執行個體發生名稱衝突，這麼做是有必要的。  
  
 自動執行個體名稱是 LocalDB 基準發行版本號碼，前面加上一個 “v” 字元。 這看起來像是 "v" 加上兩個數字，中間以句號分隔，例如 v11.0 或 V12.00。  
  
 不合法的自動執行個體名稱範例如下：  
  
-   11.0 (遺漏開頭的 “v” 字元)  
  
-   v11 (遺漏句號及第二組版本號碼)  
  
-   v11. (遺漏第二組版本號碼)  
  
-   v11.0.1.2 (版本號碼超過兩個部分)  
  
## <a name="named-localdb-instances"></a>具名 LocalDB 執行個體  
 具名 LocalDB 執行個體為「私用」；每個執行個體會由負責建立及管理該執行個體的單一應用程式所擁有。 具名 LocalDB 執行個體提供隔離並提升效能。  
  
### <a name="named-instance-creation"></a>具名執行個體建立  
 使用者建立具名執行個體時，必須透過 LocalDB 管理 API 以明確的方式建立，或透過 Managed 應用程式的 app.config 檔案以隱含的方式建立。 Managed 應用程式也可以使用 API。  
  
 每個具名執行個體具有相關聯的 LocalDB 版本；亦即指向一組指定的 LocalDB 二進位檔。 您可以在執行個體建立程序期間設定具名執行個體的版本。  
  
### <a name="named-instance-naming-rules"></a>具名執行個體命名規則  
 LocalDB 執行個體名稱最多可以包含共 128 個字元 (這是 `sysname` 資料類型加諸的限制)。 這與傳統的 SQL Server 執行個體名稱相較下十分不同，傳統的執行個體限制使用 16 個 ASCII 字元的 NetBIOS 名稱。 造成此差異的原因在於，LocalDB 將資料庫視為檔案，進而意味著以檔案為主的語意，因此使用者可以更自由地以直覺的方式選擇執行個體名稱。  
  
 LocalDB 執行個體名稱可以在檔案名稱元件內包含合法的任何 Unicode 字元。 檔案名稱元件中不合法的字元通常包含下列字元： ASCII/Unicode 字元 1 到 31，以及引號 （"）、 小於 (\<)、 大於 (>)、 直立線符號 (|)、 退格鍵 (\b)、 定位字元 (\t)、 冒號 （:）、 星號 （*）問號 （？）、 反斜線 (\\)，並正斜線 （/）。 請注意，由於 Null 字元 (\0) 用於字串結束字元，因此允許使用；將忽略第一個 Null 字元之後的所有字元。  
  
> [!NOTE]  
>  不合法的字元清單可能取決於作業系統，並且可能在未來版本中變更。  
  
 執行個體名稱中的開頭及尾端空白會予以忽略並修剪。  
  
 若要避免命名衝突，具名 LocalDB 執行個體名稱不能遵循命名模式自動執行個體，「 自動執行個體命名規則。 」 稍早所述 嘗試使用遵循自動執行個體命名模式有效的名稱建立具名執行個體建立的預設執行個體。  
  
## <a name="sql-server-express-localdb-reference-topics"></a>SQL Server Express LocalDB 參考主題  
 [SQL Server Express LocalDB 標頭和版本資訊](sql-server-express-localdb-header-and-version-information.md)  
 提供標頭檔資訊和登錄機碼，以尋找 LocalDB 執行個體 API。  
  
 [命令列管理工具：SqlLocalDB.exe](command-line-management-tool-sqllocaldb-exe.md)  
 描述 SqlLocalDB.exe，此工具可從命令列管理 LocalDB 執行個體。  
  
 [LocalDBCreateInstance 函式](localdbcreateinstance-function.md)  
 描述新建 LocalDB 執行個體的函數。  
  
 [LocalDBDeleteInstance 函式](localdbdeleteinstance-function.md)  
 描述移除 LocalDB 執行個體的函數。  
  
 [LocalDBFormatMessage 函式](localdbformatmessage-function.md)  
 描述傳回 LocalDB 錯誤之當地語系化說明的函數。  
  
 [LocalDBGetInstanceInfo 函式](localdbgetinstanceinfo-function.md)  
 描述取得 LocalDB 執行個體資訊的函數；例如，執行個體是否存在、版本資訊，執行個體是否正在執行等等。  
  
 [LocalDBGetInstances 函式](localdbgetinstances-function.md)  
 描述傳回指定版本之所有 LocalDB 執行個體的函數。  
  
 [LocalDBGetVersionInfo 函式](localdbgetversioninfo-function.md)  
 描述傳回指定版本之所有 LocalDB 執行個體的函數。  
  
 [LocalDBGetVersions 函式](localdbgetversions-function.md)  
 描述傳回電腦上所有可用之 LocalDB 版本的函數。  
  
 [LocalDBShareInstance 函式](localdbshareinstance-function.md)  
 描述共用指定 LocalDB 執行個體的函數。  
  
 [LocalDBStartInstance 函式](localdbstartinstance-function.md)  
 描述啟動指定 LocalDB 執行個體的函數。  
  
 [LocalDBStartTracing 函式](localdbstarttracing-function.md)  
 描述為使用者啟用 API 追蹤的函數。  
  
 [LocalDBStopInstance 函式](localdbstopinstance-function.md)  
 描述停止執行指定 LocalDB 執行個體的函數。  
  
 [LocalDBStopTracing 函式](localdbstoptracing-function.md)  
 描述為使用者停用 API 追蹤的函數。  
  
 [LocalDBUnshareInstance 函式](localdbunshareinstance-function.md)  
 描述停止共用指定 LocalDB 執行個體的函數。  
  
  
