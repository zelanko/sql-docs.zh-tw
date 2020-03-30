---
title: 錯誤和事件參考 (複寫) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], errors
- replication [SQL Server], troubleshooting
- errors [SQL Server replication]
- errors and events reference [SQL Server replication]
ms.assetid: e67d1bab-47b6-441d-ab9c-251a2ca499e1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 813607ed006fb38120fd4a6f565fb9d6280f10b5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "76286410"
---
# <a name="errors-and-events-reference-replication"></a>錯誤和事件參考 (複寫)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  文件集的這一部分包含導致與複寫相關的許多錯誤之原因和解決方案的資訊。  
  
|錯誤|訊息|  
|-----------|-------------|  
|[MSSQL_ENG002601](../../relational-databases/replication/mssql-eng002601.md)|無法以唯一索引 '%.\*ls' 在物件 '%.*ls' 中插入重複的索引鍵資料列。|  
|[MSSQL_ENG002627](../../relational-databases/replication/mssql-eng002627.md)|違反 %ls 條件約束 '%.*ls'。 無法在物件 '%.\*ls' 中插入重複的索引鍵。|  
|[MSSQL_ENG003165](../../relational-databases/replication/mssql-eng003165.md)|資料庫 '%ls' 已還原，不過在還原/移除複寫時發生錯誤。 資料庫已保持離線。 請參閱《SQL Server 線上叢書》中的主題＜MSSQL_ENG003165＞。|  
|[MSSQL_ENG003724](../../relational-databases/replication/mssql-eng003724.md)|無法 %S_MSG %S_MSG '%.*ls'，因為它正用於複寫。|  
|[MSSQL_ENG004929](../../relational-databases/replication/mssql-eng004929.md)|無法改變 %S_MSG '%.*ls'，因為它正在為複寫而發行。|  
|MSSQL_ENG007395。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|無法為連結伺服器 "%ls" 的 OLE DB 提供者 "%ls" 啟動巢狀交易。 因為 XACT_ABORT 選項已設定為 OFF，所以必須要有巢狀交易。|  
|[MSSQL_ENG014005](../../relational-databases/replication/mssql-eng014005.md)|無法卸除發行集。 有它的訂閱存在。|  
|[MSSQL_ENG014010](../../relational-databases/replication/mssql-eng014010.md)|伺服器 '%s' 並未定義為訂閱伺服器。|  
|[MSSQL_ENG014114](../../relational-databases/replication/mssql-eng014114.md)|'%s' 並未設定為散發者。|  
|[MSSQL_ENG014117](../../relational-databases/replication/mssql-eng014117.md)|'%s' 並未設定為散發資料庫。|  
|[MSSQL_ENG014120](../../relational-databases/replication/mssql-eng014120.md)|無法卸除散發資料庫 '%s'。 這個散發資料庫與一發行者相關聯。|  
|[MSSQL_ENG014121](../../relational-databases/replication/mssql-eng014121.md)|無法卸除散發者 '%s'。 這個散發者有相關聯的散發資料庫。|  
|[MSSQL_ENG014144](../../relational-databases/replication/mssql-eng014144.md)|無法卸除訂閱者 '%s'。 發行集資料庫 '%s' 中有其訂閱。|  
|[MSSQL_ENG014150](../../relational-databases/replication/mssql-eng014150.md)|複寫 -%s：代理程式 %s 成功。 %s|  
|[MSSQL_ENG014151](../../relational-databases/replication/mssql-eng014151.md)|複寫 -%s：代理程式 %s 失敗。 %s|  
|[MSSQL_ENG014152](../../relational-databases/replication/mssql-eng014152.md)|複寫 -%s：代理程式 %s 已排程重試。 %s|  
|[MSSQL_ENG014157](../../relational-databases/replication/mssql-eng014157.md)|由訂閱者 '%s' 建立給發行集 '%s' 的訂閱已經過期且已經卸除。|  
|[MSSQL_ENG014160](../../relational-databases/replication/mssql-eng014160.md)|已設定針對發行集[%s]的臨界值[%s:%s] 此發行集的一個或多個訂閱已經到期。|  
|[MSSQL_ENG014161](../../relational-databases/replication/mssql-eng014161.md)|已設定針對發行集[%s]的臨界值[%s:%s] 請確定記錄讀取器和散發代理程式正在執行，而且符合延遲需求。|  
|[MSSQL_ENG014162](../../relational-databases/replication/mssql-eng014162.md)|已設定針對發行集[%s]的臨界值[%s:%s] 請確定合併代理程式正在執行，而且符合預期需求。|  
|[MSSQL_ENG014163](../../relational-databases/replication/mssql-eng014163.md)|已設定針對發行集[%s]的臨界值[%s:%s] 請確定合併代理程式正在執行，而且符合預期需求。|  
|[MSSQL_ENG014164](../../relational-databases/replication/mssql-eng014164.md)|已設定針對發行集[%s]的臨界值[%s:%s] 請確定合併代理程式正在執行，而且符合預期需求。|  
|[MSSQL_ENG014165](../../relational-databases/replication/mssql-eng014165.md)|已設定針對發行集[%s]的臨界值[%s:%s] 請確定合併代理程式正在執行，而且符合預期需求。|  
|[MSSQL_ENG018456](../../relational-databases/replication/mssql-eng018456.md)|使用者 '%.*ls'.%.\*ls 登入失敗|  
|[MSSQL_ENG018752](../../relational-databases/replication/mssql-eng018752.md)|一次只有一個記錄讀取器代理程式或記錄檔相關程序 (sp_repldone, sp_replcmds, and sp_replshowcmds) 可連接到資料庫。 若您已執行記錄檔相關程序，請卸除執行程序的連接，或者利用該連接執行 sp_replflush 之後，再啟動記錄讀取器代理程式或執行其他記錄檔相關程序。|  
|[MSSQL_ENG020554](../../relational-databases/replication/mssql-eng020554.md)|複寫代理程式已有 %ld 分鐘未記錄進度訊息。 這可能表示代理程式沒有回應或系統活動量很高。 請確認記錄正在複寫至目的地，而且到訂閱者、發行者及散發者的連接仍在使用中。|  
|[MSSQL_ENG020557](../../relational-databases/replication/mssql-eng020557.md)|代理程式關閉。 如需詳細資訊，請參閱 SQL Server Agent 作業記錄中的作業 '%s'。|  
|[MSSQL_ENG020572](../../relational-databases/replication/mssql-eng020572.md)|訂閱者 '%s' 訂閱的發行項 '%s' (在發行集 '%s' 中)，已經在驗證失敗後重新初始化。|  
|[MSSQL_ENG020574](../../relational-databases/replication/mssql-eng020574.md)|訂閱者 '%s' 訂閱的發行項 '%s' (在發行集 '%s' 中)，未通過資料驗證。|  
|[MSSQL_ENG020575](../../relational-databases/replication/mssql-eng020575.md)|訂閱者 '%s' 訂閱的發行項 '%s' (在發行集 '%s' 中)，已通過資料驗證。|  
|[MSSQL_ENG020596](../../relational-databases/replication/mssql-eng020596.md)|只有 '%s' 或 db_owner 的成員可以卸除匿名的代理程式。|  
|[MSSQL_ENG020598](../../relational-databases/replication/mssql-eng020598.md)|套用複寫命令時，在訂閱者端找不到資料列。|  
|[MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md)|發行集 '%s' 的初始快照集尚無法使用。|  
|[MSSQL_ENG021076](../../relational-databases/replication/mssql-eng021076.md)|發行項 '%s' 的初始快照集仍然無法使用。|  
|[MSSQL_ENG021286](../../relational-databases/replication/mssql-eng021286.md)|衝突資料表 '%s' 不存在。|  
|[MSSQL_ENG021330](../../relational-databases/replication/mssql-eng021330.md)|無法在複寫工作目錄下建立子目錄。(%ls)|  
|[MSSQL_ENG021331](../../relational-databases/replication/mssql-eng021331.md)|無法將使用者指令碼檔案複製到散發者。(%ls)|  
|[MSSQL_ENG021385](../../relational-databases/replication/mssql-eng021385.md)|快照集無法處理發行集 '%s'。 可能是由於有使用中的結構描述變更活動，或是正在加入新的發行項。|  
|MSSQL_ENG021617。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|無法執行 SQL*PLUS。 請確認散發者端已安裝目前版本的 Oracle 用戶端程式碼。|  
|MSSQL_ENG021620。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|可透過系統 Path 變數存取的 SQL*PLUS 版本，目前不足以支援 Oracle 發行。 請確認散發者端已安裝目前版本的 Oracle 用戶端程式碼。|  
|MSSQL_ENG021624。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|在散發者 '%s' 端找不到已註冊的 Oracle OLEDB 提供者 (OraOLEDB.Oracle)。 請確認已安裝目前版本的 Oracle OLEDB 提供者，並在散發者端註冊。|  
|MSSQL_ENG021626。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|無法使用 Oracle OLEDB 提供者 (OraOLEDB.Oracle) 連接到 Oracle 資料庫伺服器 '%s'。|  
|MSSQL_ENG021627。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|無法使用 Microsoft OLEDB 提供者 (MSDAORA) 連接到 Oracle 資料庫伺服器 '%s'。|  
|MSSQL_ENG021628。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|無法更新散發者 '%s' 的登錄，以允許使用 SQL Server 在處理序中執行 Oracle OLEDB 提供者 (OraOLEDB.Oracle)。 請確認目前的登入已獲得授權，可修改 SQL Server 擁有的登錄機碼。|  
|MSSQL_ENG021629。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|CLSID 登錄機碼指出散發者端沒有已經註冊的 Oracle OLEDB Provider for Oracle (OraOLEDB.Oracle)。 請確認已安裝 Oracle OLEDB 提供者，並在散發者端註冊。|  
|MSSQL_ENG021642。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|異質性發行者需要已連結伺服器。 已經存在名稱為 '%s' 的連結伺服器。 請移除連結的伺服器或選擇其他發行者名稱。|  
|MSSQL_ENG021663。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|找不到有效的來源資料表 [%s].[%s] 主索引鍵。|  
|MSSQL_ENG021684。 請參閱 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。|與 Oracle 發行者 '%s' 管理者登入相關聯的權限不足。|  
|[MSSQL_ENG021797](../../relational-databases/replication/mssql-eng021797.md)|'%s' 必須是有效的 Windows 登入，其格式為：'MACHINE\Login' 或 'DOMAIN\Login'。 請參閱 '%s' 的文件集。|  
|[MSSQL_ENG021798](../../relational-databases/replication/mssql-eng021798.md)|在繼續進行之前，必須先經由 '%s' 將 '%s' 代理程式作業加入。 請參閱 '%s' 的文件集。|  
|[MSSQL_REPL020011](../../relational-databases/replication/mssql-repl020011.md)|該處理無法執行 '%1' (在 '%2')。|  
|[MSSQL_REPL027056](../../relational-databases/replication/mssql-repl027056.md)|合併處理無法變更生成集記錄 '%1'。 執行疑難排解時，以詳細資訊記錄重新啟動同步處理，並指定要寫入的輸出檔案。|  
|[MSSQL_REPL027183](../../relational-databases/replication/mssql-repl027183.md)|合併處理無法以參數化資料列篩選器來列舉發行項的變更。 如果這個失敗繼續發生，請增加這個處理的查詢逾時、縮短發行集的保留期限，以及改善發行資料表的索引。|  
  
  
