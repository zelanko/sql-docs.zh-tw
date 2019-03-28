---
title: 控制交易持久性 | Microsoft 文件
ms.custom: ''
ms.date: 05/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- delayed durability
- Lazy Commit
ms.assetid: 3ac93b28-cac7-483e-a8ab-ac44e1cc1c76
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a90d40b158acf786ccb5bcdf962c2d6077c59dd
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535180"
---
# <a name="control-transaction-durability"></a>控制交易持久性
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易認可可能是完全持久 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設值) 或延遲的持久 (也稱為延遲認可)。  
  
 完全持久交易認可是同步認可，而且只有在交易的記錄檔記錄寫入磁碟之後，才會將認可回報為成功並將控制權傳回給用戶端。 延遲的持久交易認可是非同步認可，而且在交易的記錄檔記錄寫入磁碟之前，就會將認可回報為成功。 將交易記錄項目寫入磁碟是讓交易能夠持久的必要條件。 延遲的持久交易會在交易記錄項目排清至磁碟時變成持久。  
  
 本主題將詳細說明延遲的持久交易。  
  
## <a name="full-vs-delayed-transaction-durability"></a>完全與延遲的交易持久性  
 完全與延遲的交易持久性各有其優缺點。 應用程式可以混合使用完全與延遲的持久交易。 您應該仔細考量業務需求，以及每種交易如何配合這些需求。  
  
### <a name="full-transaction-durability"></a>完全交易持久性  
 完全持久交易會先將交易記錄寫入磁碟，然後再將控制權傳回給用戶端。 只要符合下列情況，您就應該使用完全持久交易：  
  
-   您的系統無法容忍任何資料遺失。   
    如需何時會遺失部分資料的相關資訊，請參閱 [我何時會遺失資料？](#when-can-i-lose-data) 一節。  
  
-   造成瓶頸的原因不是交易記錄寫入延遲。  
  
 延遲的交易持久性可減少記錄 I/O 造成的延遲，方法是將交易記錄檔記錄保留在記憶體中，並且批次寫入交易記錄，因此需要的 I/O 作業較少。 延遲的交易持久性可能會減少記錄 I/O 競爭，因而減少系統的等候時間。  
  
 **完全交易持久性保證**  
  
-   一旦交易認可成功之後，系統中的其他交易就可以看到該筆交易所進行的變更。 請參閱主題[交易隔離等級](../../database-engine/transaction-isolation-levels.md)如需詳細資訊。  
  
-   持久性是在認可時獲得保證。 在交易認可成功並將控制權傳回給用戶端之前，對應的記錄檔記錄都會保存到磁碟。  
  
### <a name="delayed-transaction-durability"></a>延遲的交易持久性  
 延遲的交易持久性是使用磁碟的非同步記錄寫入來達成。 交易記錄檔記錄會保留在緩衝區中，然後在緩衝區填滿或發生緩衝區排清事件時寫入磁碟。 延遲的交易持久性會同時減少系統中的延遲和競爭，因為：  
  
-   交易認可處理不會等候記錄 IO 完成並將控制權傳回給用戶端。  
  
-   並行交易不太可能會爭用記錄 IO。不過，記錄緩衝區可能會以較大的區塊排清至磁碟，以便減少競爭並提高輸送量。  
  
    > [!NOTE]  
    >  如果並行程度很高，仍然可能會發生記錄 I/O 競爭，尤其是記錄緩衝區的填滿速度比排清速度快時。  
  
 **何時使用延遲的交易持久性**  
  
 可因使用延遲的交易持久性而獲益的情形如下：  
  
 **您可以容忍部分資料遺失。**  
 如果您可以容忍部分資料遺失 (只要擁有大部分資料即可，個別記錄並不重要)，延遲的持久性就值得考慮使用。 如果您無法容忍任何資料遺失，請勿使用延遲的交易持久性。  
  
 **您會在交易記錄寫入時遇到瓶頸。**  
 如果您的效能問題是由於交易記錄寫入的延遲所造成，則使用延遲的交易持久性可能會讓您的應用程式從中獲益。  
  
 **您的工作負載具有很高的競爭率。**  
 如果您的系統具有高競爭層級的工作負載，就表示花很多時間在等候釋放鎖定。 延遲的交易持久性會減少認可時間並加快釋放鎖定的速度，因而提高輸送量。  
  
 **延遲交易持久性保證**  
  
-   一旦交易認可成功之後，系統中的其他交易就可以看到該筆交易所進行的變更。  
  
-   只有在記憶體中的交易記錄排清至磁碟之後，才會保證交易持久性。 記憶體中的交易記錄會在下列情況中排清至磁碟：  
  
    -   相同資料庫中的完全持久交易對資料庫進行變更並且成功認可。  
  
    -   使用者成功執行系統預存程序 `sp_flush_log`。  
  
    -   記憶體中的交易記錄緩衝區填滿並自動排清至磁碟。  
  
     如果完全持久交易或 sp_flush_log 成功認可，就表示所有先前認可的延遲持久交易都已經變成持久。  
  
 記錄可能會定期排清到磁碟。 但是，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會提供持久交易和 sp_flush_log 以外的任何持久性保證。  
  
## <a name="how-to-control-transaction-durability"></a>如何控制交易持久性  
  
### <a name="database-level-control"></a>資料庫層級控制  
 身為 DBA 的您，可以控制使用者是否能使用下列陳述式，在資料庫上使用延遲的交易持久性。 您必須使用 ALTER DATABASE 來設定延遲的持久性設定。  
  
```sql  
ALTER DATABASE ... SET DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
```  
  
 `DISABLED`  
 [預設值] 使用這項設定時，在資料庫上認可的所有交易都是完全持久，不論認可層級設定為何 (DELAYED_DURABILITY=[ON | OFF])。 完全不需要進行預存程序變更和重新編譯。 這可讓您確保任何資料都不會因為延遲的持久性而面臨風險。  
  
 `ALLOWED`  
 使用這項設定時，每筆交易的持久性都是在交易層級上決定的 - DELAYED_DURABILITY = { *OFF* | ON }。 請參閱[不可部分完成的區塊層級控制-原生編譯預存程序](#atomic-block-level-control---natively-compiled-stored-procedures)並[認可層級控制-Transact SQL](#commit-level-control---t-sql)如需詳細資訊。  
  
 `FORCED`  
 使用這項設定時，在資料庫上認可的每筆交易都是延遲的持久。 不論交易是否有指定完全持久 (DELAYED_DURABILITY = OFF) ，交易都是延遲的持久。 當延遲的交易持久性適用於資料庫，而且您不想要變更任何應用程式程式碼時，這項設定就很有用。  
  
### <a name="atomic-block-level-control---natively-compiled-stored-procedures"></a>不可部分完成的區塊層級控制-原生編譯預存程序  
 下列程式碼會進入不可部分完成的區塊內部。  
  
```sql  
DELAYED_DURABILITY = { OFF | ON }  
```  
  
 `OFF`  
 [預設值] 交易是完全持久，除非資料庫選項 DELAYED_DURABLITY = FORCED 作用中，此時認可就是非同步，因而成為延遲的持久。 如需相關資訊，請參閱 [Database level control](#database-level-control) 。  
  
 `ON`  
 交易是延遲的持久，除非資料庫選項 DELAYED_DURABLITY = DISABLED 作用中，此時認可就是同步，因而成為完全持久。  如需相關資訊，請參閱 [Database level control](#database-level-control) 。  
  
 **範例程式碼：**  
  
```sql  
CREATE PROCEDURE <procedureName> ...  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
    DELAYED_DURABILITY = ON,  
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'English'  
    ...  
)  
END  
```  
  
### <a name="table-1-durability-in-atomic-blocks"></a>表 1：不可部分完成之區塊的持久性  
  
|不可部分完成的區塊持久性選項|無現有的交易|交易處理中 (完全或延遲的持久)|  
|------------------------------------|-----------------------------|---------------------------------------------------------|  
|`DELAYED_DURABILITY = OFF`|不可部分完成的區塊會啟動新的完全持久交易。|不可部分完成的區塊會在現有的交易中建立儲存點，然後開始新的交易。|  
|`DELAYED_DURABILITY = ON`|不可部分完成的區塊會啟動新的延遲持久交易。|不可部分完成的區塊會在現有的交易中建立儲存點，然後開始新的交易。|  
  
### <a name="commit-level-control---t-sql"></a>COMMIT 層級控制-(T-SQL)
 COMMIT 語法已擴充，因此您可以強制延遲的交易持久性。 如果資料庫層級的 DELAYED_DURABILITY 是 DISABLED 或 FORCED (請參閱上述說明)，就會忽略這個 COMMIT 選項。  
  
```sql  
COMMIT [ { TRAN | TRANSACTION } ] [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]  
  
```  
  
 `OFF`  
 [預設值] 交易 COMMIT 是完全持久，除非資料庫選項 DELAYED_DURABLITY = FORCED 作用中，此時 COMMIT 就是非同步，因而成為延遲的持久。 如需相關資訊，請參閱 [Database level control](#database-level-control) 。  
  
 `ON`  
 交易 COMMIT 是延遲的持久，除非資料庫選項 DELAYED_DURABLITY = DISABLED 作用中，此時 COMMIT 就是同步，因而成為完全持久。 如需相關資訊，請參閱 [Database level control](#database-level-control) 。  
  
### <a name="summary-of-options-and-their-interactions"></a>選項及其互動的摘要  
 下表將摘要說明資料庫層級延遲的持久性設定與認可層級設定之間的互動。 資料庫層級設定一律優先於認可層級設定。  
  
|COMMIT 設定/資料庫設定|DELAYED_DURABILITY = DISABLED|DELAYED_DURABILITY = ALLOWED|DELAYED_DURABILITY = FORCED|  
|--------------------------------------|-------------------------------------|------------------------------------|-----------------------------------|  
|`DELAYED_DURABILITY = OFF` 資料庫層級交易。|交易是完全持久。|交易是完全持久。|交易是延遲的持久。|  
|`DELAYED_DURABILITY = ON` 資料庫層級交易。|交易是完全持久。|交易是延遲的持久。|交易是延遲的持久。|  
|`DELAYED_DURABILITY = OFF` 跨資料庫或分散式交易。|交易是完全持久。|交易是完全持久。|交易是完全持久。|  
|`DELAYED_DURABILITY = ON` 跨資料庫或分散式交易。|交易是完全持久。|交易是完全持久。|交易是完全持久。|  
  
## <a name="how-to-force-a-transaction-log-flush"></a>如何強制交易記錄排清  
 強制將交易記錄排清至磁碟的方法有兩種。  
  
-   執行任何更改相同資料庫的完全持久交易。 這會強制將所有先前認可之延遲持久交易的記錄檔記錄排清至磁碟。  
  
-   執行系統預存程序 `sp_flush_log`。 這個程序會強制將所有先前認可之延遲持久交易的記錄檔記錄排清至磁碟。 如需詳細資訊，請參閱 [sys.sp_flush_log &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-flush-log-transact-sql)。  
  
##  <a name="delayed-durability-and-other-sql-server-features"></a>延遲的持久性和其他 SQL Server 功能  
 **變更追蹤與變更資料擷取**  
 所有具有變更追蹤的交易都是完全持久。 如果某筆交易會對啟用變更追蹤的資料表進行任何寫入作業，它就具有變更追蹤屬性。 不支援使用異動資料擷取 (CDC) 之資料庫的延遲持久性。   
  
 **當機復原**  
 保證一致性，但是來自已經認可之延遲持久交易的某些變更可能會遺失。  
  
 **跨資料庫和 DTC**  
 如果某筆交易是跨資料庫或分散式交易，不論任何資料庫或交易認可設定為何，它都是完全持久。  
  
 **Always On 可用性群組和鏡像**  
 延遲的持久交易無法在主要或任何次要資料庫上保證任何持久性。 此外，它們無法保證任何關於次要資料庫上交易的知識。 認可之後，從任何同步的次要收到任何確認之前，就會將控制權傳回給用戶端。  
  
 **容錯移轉叢集**  
 某些延遲的持久交易寫入可能會遺失。  
  
 **異動複寫**  
 異動複寫不支援延遲的持久交易。  
  
 **記錄傳送**  
 只有已經變成持久的交易才會包含在傳送的記錄中。  
  
 **記錄備份**  
 只有已經變成持久的交易才會包含在備份中。  
  
## <a name="when-can-i-lose-data"></a>我何時會遺失資料？  
 如果您在任何資料表上實作延遲持久性，您應該了解特定環境會導致資料遺失。 如果您無法容忍任何資料遺失，就不應該在資料表中使用延遲持久性。  
  
### <a name="catastrophic-events"></a>重大事件  
 發生重大事件 (例如伺服器當機) 時，您將遺失所有尚未儲存到磁碟的已認可交易資料。 每當針對資料表中的任何資料表 (持久性記憶體最佳化或以磁碟為基礎的資料表) 執行完全持久交易，或呼叫 `sp_flush_log` 時，即會將延遲的持久交易儲存到磁碟。 如果您正在使用延遲的持久交易，您可以在資料庫中建立小型資料表，以便定期更新或定期呼叫 `sp_flush_log` 來儲存所有尚未認可完畢的交易。 交易記錄也會在它已滿時排清，但這很難預期且無法控制。  
  
### <a name="sql-server-shutdown-and-restart"></a>SQL Server 關機並重新啟動  
 針對延遲的持久性， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的意外關機與預期的關機/重新啟動之間並無差異。 就像重大事件一樣，您應該針對資料遺失進行規劃。 在規劃好的關機/重新啟動中，部分尚未寫入磁碟的交易可能會先儲存到磁碟，但您不應該規劃相關事項。 對於類似關機/重新啟動的規劃 (不論是規劃或未規劃的) 都會像重大事件一樣遺失資料。  
  
## <a name="see-also"></a>另請參閱  
 [交易隔離等級](../../database-engine/transaction-isolation-levels.md)   
 [搭配經記憶體最佳化的資料表使用交易隔離等級的方針](../in-memory-oltp/memory-optimized-tables.md)  
  
  
