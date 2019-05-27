---
title: 針對全文檢索索引進行疑難排解 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- indexes [full-text search]
- troubleshooting [SQL Server], full-text search
- troubleshooting [full-text search]
ms.assetid: 964c43a8-5019-4179-82aa-63cd0ef592ef
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cd7ce157e831d32272f6ff2531c39f789a01e901
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66015084"
---
# <a name="troubleshoot-full-text-indexing"></a>疑難排解全文檢索索引
     
##  <a name="failure"></a> 疑難排解全文檢索索引失敗  
 擴展或維護全文檢索索引時，全文檢索索引子可能會因為下面所描述的原因而無法對一個或多個資料列進行檢索。 這些資料列層級錯誤不會讓母體擴展無法完成。 索引子會略過這些資料列，而這表示您無法查詢這些資料列中所含的內容。  
  
 下列情況可能會發生編製索引失敗：  
  
-   索引子找不到或無法載入篩選或斷詞工具元件。 如果資料表資料列包含尚未向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體註冊之某個語言的文件格式或內容，會發生此失敗。 在載入已註冊的斷詞工具或篩選元件時，如果該元件尚未進行簽署或無法進行簽章驗證，也會發生此失敗。  
  
-   元件 (例如斷詞工具或篩選) 失敗，並將錯誤傳回給索引子。 如果正在進行檢索的文件損毀，且篩選無法從文件中擷取文字，則會發生這個狀況。 當元件無法處理超過特定大小之單一資料列的內容時 (因全文檢索篩選背景程式主機 (fdhost.exe) 的記憶體限制)，也可能發生這個狀況。  
  
 搜耙記錄檔會包含每個資料列層級失敗原因的詳細資料。 且會在完整或累加母體擴展結束時彙總說明錯誤計數。  
  
 其他失敗也會影響編製索引處理序本身，並讓母體擴展無法完成。  
  
-   全文檢索索引超出全文檢索目錄中可含之資料列數的限制。  
  
-   變更、捨棄或重建正在檢索之資料表上的叢集索引或全文檢索索引鍵索引。  
  
-   硬體故障或磁碟損毀導致全文檢索目錄損毀。  
  
-   內含在進行全文檢索索引之資料表的檔案群組離線或變成唯讀。  
  
 您應該在結束任何大量全文檢索索引母體擴展作業時，或發現母體擴展未完成時，檢視搜耙記錄檔。  
  
### <a name="unsigned-components"></a>未簽署的元件  
 依預設，全文檢索索引子需要有它可載入以進行簽署的篩選和斷詞工具。 如果這些元件未進行簽署，則有時安裝自訂元件時，您必須設定全文檢索索引子以略過簽章驗證。  
  
> [!IMPORTANT]  
>  略過簽章驗證會讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體變得較不安全。 建議您簽署任何所實作的元件，或確定所取得的任何元件都已進行簽署。 如需簽署元件的資訊，請參閱 [sp_fulltext_service &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)。  
  

  
##  <a name="state"></a> 全文檢索索引在還原交易記錄之後處於不一致的狀態  
 當復原資料庫的交易記錄時，您會看到一個警告，指出全文檢索索引處於不一致的狀態。 原因是備份資料庫後，資料表的全文檢索索引已發生變更。 若要讓全文檢索索引的狀態一致，您必須在資料表上執行完整母體擴展 (搜耙)。 如需詳細資訊，請參閱 [擴展全文檢索索引](../indexes/indexes.md)。  
  

  
## <a name="see-also"></a>另請參閱  
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)   
 [擴展全文檢索索引](../indexes/indexes.md)  
  
  
