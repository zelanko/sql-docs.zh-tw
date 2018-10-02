---
title: 在異動複寫中發行預存程序執行 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], stored procedures and
- transactional replication, publishing stored procedure execution
ms.assetid: f4686f6f-c224-4f07-a7cb-92f4dd483158
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85643186d92e2033fc909ae166533cac0e18f44d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732706"
---
# <a name="publishing-stored-procedure-execution-in-transactional-replication"></a>在異動複寫中發行預存程序執行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果您有一或多個預存程序在「發行者」端執行並且影響到已發行的資料表，請考慮在發行集中包含這些預存程序，以做為預存程序執行發行項。 初始化訂閱時，會將程序的定義 (CREATE PROCEDURE 陳述式) 複寫到訂閱者；在發行者端執行程序時，複寫會在訂閱者端執行對應的程序。 這可在執行大批量作業時大幅提升效能，因為只會複寫程序執行，而無需複寫每個資料列的個別變更。 例如，假設您在發行集資料庫中建立了下列預存程序：  
  
```  
CREATE PROC give_raise AS  
UPDATE EMPLOYEES SET salary = salary * 1.10  
```  
  
 此程序讓公司的 10,000 位員工每人增加 10% 的收入。 當您在「發行者」執行此預存程序，它會更新每一位員工的薪水。 沒有預存程序執行複寫時，更新會傳送到「訂閱者」，做為較大的多步驟交易：  
  
```  
BEGIN TRAN  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 1'  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 2'  
```  
  
 然後重複 10,000 次，完成所有更新。  
  
 有預存程序執行複寫時，複寫僅傳送命令以在「訂閱者」端執行預存程序，而不會將所有更新寫入散發資料庫，然後透過網路將它們傳送到「訂閱者」：  
  
```  
EXEC give_raise  
```  
  
> [!IMPORTANT]  
>  預存程序複寫並不適用於所有應用程式。 如果發行項經水平篩選，以使「發行者」與「訂閱者」端的資料列組不同，則在兩端執行相同的預存程序將傳回不同的結果。 同樣地，如果更新是基於其他非複寫資料表的子查詢，則在「發行者」和「訂閱者」端執行相同的預存程序也將傳回不同的結果。  
  
 **若要發行預存程序的執行**  
  
-   SQL Server Management Studio：[在交易式發行集中發行預存程序的執行項 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
-   複寫 Transact-SQL 程式設計：執行 [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)，並指定值 'serializable proc exec' (建議) 或為參數 **@type** 指定 'proc exec'。 如需定義發行項的詳細資訊，請參閱[定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## <a name="modifying-the-procedure-at-the-subscriber"></a>在訂閱者端修改程序  
 根據預設值，「發行者」的預存程序定義會傳播到各個「訂閱者」。 但是，您也可以在「訂閱者」端修改預存程序。 若您想在「發行者」和「訂閱者」執行不同的邏輯，這個方式就非常有幫助。 例如，考慮 **sp_big_delete**這個「發行者」的預存程序有兩個功能：它會從複寫資料表 **big_table1** 刪除 1,000,000 個資料列，然後更新非複寫的資料表 **big_table2**。 若要降低網路資源的需求，您應該透過發行 **sp_big_delete**，將一百萬個資料列刪除做為預存程序傳播。 在「訂閱者」端，您可以將 **sp_big_delete** 修改為只刪除一百萬個資料列，並且不執行後續對 **big_table2**的更新。  
  
> [!NOTE]  
>  依預設，使用 ALTER PROCEDURE 在「發行者」上所作的任何變更都將傳播到「訂閱者」。 若要防止發生這種情況，請在執行 ALTER PROCEDURE 之前停用結構描述變更的傳播。 如需結構描述變更的資訊，請參閱[對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## <a name="types-of-stored-procedure-execution-articles"></a>預存程序執行發行項的類型  
 可以透過兩種不同方式發行預存程序的執行：序列化程序執行發行項與程序執行發行項。  
  
-   建議使用序列化方式，因為這種方式只有當程序在序列化交易的內容中執行時，才會複寫程序執行。 若預存程序從序列化交易外部執行時，對已發行的資料表中所做的資料變更，會複寫為一連串的 DML 陳述式。 這個行為保證「訂閱者」的資料可以和「發行者」的資料一致。 這個方法對於批次作業而言特別有用，例如大型的清除作業。  
  
-   利用程序執行選項可以將執行複寫到所有「訂閱者」，而不管預存程序中的個別陳述式是否成功。 此外，因為預存程序對資料所做的變更，可以發生在多個交易中，「訂閱者」的資料可能不會與「發行者」的資料一致。 若要處理這些問題，「訂閱者」必須是唯讀的，而且您所使用的隔離等級必須大於讀取未認可。 如果您使用讀取未認可，則對已發行資料表中所做的資料變更會複寫為一連串的 DML 陳述式。  
  
 以下範例說明當您將程序的複寫設定為序列化程序發行項 (Article) 時的建議方式。  
  
```  
BEGIN TRANSACTION T1  
SELECT @var = max(col1) FROM tableA  
UPDATE tableA SET col2 = <value>   
   WHERE col1 = @var   
  
BEGIN TRANSACTION T2  
INSERT tableA VALUES <values>  
COMMIT TRANSACTION T2  
```  
  
 上面的範例假設交易 T1 的 SELECT 比交易 T2 的 INSERT 先發生。  
  
 如果程序並非在序列化交易內執行 (隔離等級設定為 SERIALIZABLE)，交易 T2 便可插入新的資料列到 T1 的 SELECT 陳述式範圍內，並在 T1 之前認可。 這也表示 T2 會比 T1 先套用於「訂閱者」。 當 T1 套用於「訂閱者」時，SELECT 傳回的值可能和位於「發行者」時的值不同，並且可能導致 UPDATE 產生不同的結果。  
  
 如果程序執行於序列化交易內，交易 T2 則不被允許在 T2 的 SELECT 陳述式所涵蓋的範圍內插入。 此動作會被封鎖直到 T1 認可而確保「訂閱者」有相同的結果為止。  
  
 當您在序列化交易內執行程序時，鎖定的時間更長且可能導致並行性降低。  
  
## <a name="the-xactabort-setting"></a>XACT_ABORT 設定  
 複寫預存程序執行時，執行預存程序之工作階段的設定應將 XACT_ABORT 指定為 ON。 如果 XACT_ABORT 設定為 OFF，並在「發行者」端執行程序時出現錯誤，則「訂閱者」端也會出現相同的錯誤，導致「散發代理程式」失敗。 將 XACT_ABORT 指定為 ON 可確保「發行者」端執行期間遇到的任何錯誤，都會使整個執行回復，以避免「散發代理程式」失敗。 如需設定 XACT_ABORT 的詳細資訊，請參閱 [SET XACT_ABORT &#40;Transact-SQL&#41;](../../../t-sql/statements/set-xact-abort-transact-sql.md)。  
  
 如果您需要將 XACT_ABORT 設定為 OFF，請指定「散發代理程式」的 **-SkipErrors** 參數。 這將允許代理程式在遇到錯誤後，繼續在「訂閱者」端套用變更。  
  
## <a name="see-also"></a>另請參閱  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
