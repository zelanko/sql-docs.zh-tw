---
title: 針對合併發行項實作自訂衝突解析程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], stored procedure-based resolvers
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b36d610912f518f0586739e0380e300efefbed40
ms.sourcegitcommit: 3d189b68c0965909d167de61546b574af1ef7a96
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2019
ms.locfileid: "69561144"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>針對合併發行項實作自訂衝突解析程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或[以 COM 為基礎的自訂解析程式](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中針對合併發行項實作自訂衝突解決器。  
  
 **本主題內容**  
  
-   **針對合併發行項實作自訂衝突解析程式，使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [以 COM 為基礎的解析程式](#COM)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以將自訂衝突解決器撰寫為每一個發行者上的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序。 在同步處理期間，當解析程式註冊到的發行項中發生衝突時，就會叫用這個預存程序。 衝突資料列的相關資訊會由合併代理程式傳遞至程序的必要參數。 一定會在發行者上建立以預存程序為基礎的自訂衝突解決器。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序解析程式的叫用目的，只是為了處理資料列變更衝突。 這些解析程式不能用於處理其他類型的衝突，例如因 PRIMARY KEY 違規或唯一索引條件約束違規而觸發的插入失敗。
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>建立以預存程序為基礎的自訂衝突解決器  
  
1.  在發行集或 **msdb** 資料庫的發行者上，建立新的系統預存程序，以實作下列必要的參數：  
  
    |參數|資料類型|Description|  
    |---------------|---------------|-----------------|  
    |**\@tableowner**|**sysname**|解決衝突所針對之資料表的擁有者名稱。 這是發行集資料庫中資料表的擁有者。|  
    |**\@tablename**|**sysname**|解決衝突所針對之資料表的名稱。|  
    |**\@rowguid**|**uniqueidentifier**|發生衝突之資料列的唯一識別碼。|  
    |**\@subscriber**|**sysname**|傳播衝突變更所在的伺服器名稱。|  
    |**\@subscriber_db**|**sysname**|傳播衝突變更所在的資料庫名稱。|  
    |**\@log_conflict OUTPUT**|**int**|設定合併處理是否應該記錄衝突供稍後解決之用：<br /><br /> **0** = 不記錄衝突。<br /><br /> **1** = 訂閱者為衝突失敗者。<br /><br /> **2** = 發行者為衝突失敗者。|  
    |**\@conflict_message OUTPUT**|**nvarchar(512)**|當記錄衝突時，要提供之有關解決方法的訊息。|  
    |**\@destowner**|**sysname**|訂閱者上發行之資料表的擁有者。|  
  
     這個預存程序會使用由合併代理程式傳遞給這些參數的值，來實作您的自訂衝突解析邏輯。 它必須將結構中與基底資料表相同的單一資料列結果集傳回，且包含獲勝版本資料列的資料值。  
  
2.  將預存程序的 EXECUTE 權限授與給訂閱者使用的任何登入，以連接到發行者。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

#### <a name="use-a-custom-conflict-resolver-with-a-new-table-article"></a>搭配新的資料表發行項使用自訂衝突解析程式  
  
1. 執行 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 以定義發行項。 
1. 為 **\@article_resolver** 參數指定 **MicrosoftSQL** **伺服器預存程序解析程式**的值。 
1. 指定實作 **\@resolver_info** 參數的衝突解析程式邏輯的預存程序名稱。 

   如需詳細資訊，請參閱[定義發行項](../../relational-databases/replication/publish/define-an-article.md)。
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>搭配現有的資料表發行項使用自訂衝突解決器  
  
1.  執行 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)，針對 **\@property** 指定 **\@publication**、 **\@article** 及 **article_resolver** 值，並為 **\@value** 指定 [Microsoft SQL 伺服器預存程序]   值。  
  
2.  執行 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)，針對 **\@property** 指定 **\@publication**、 **\@article** 以及 **resolver_info** 值，並針對 **\@value** 命名實作衝突解析程式邏輯的預存程序名稱。  
  
##  <a name="COM"></a> 使用以 COM 為基礎的自訂解析程式  
 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 命名空間會實作一個介面，此介面可讓您撰寫複雜的商務邏輯來處理事件，並解決合併複寫同步處理程序期間所發生的衝突。 如需詳細資訊，請參閱[為合併發行項實作商務邏輯處理常式](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。 您也可以撰寫自己的原生程式碼式自訂商務邏輯，以解決衝突。 此邏輯會建置為 COM 元件，並編譯成動態連結程式庫 (DLL) (使用如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++ 的產品)。 這種以 COM 為基礎的自訂衝突解析程式必須實作 **ICustomResolver** 介面，此介面是專門針對衝突解決所設計。  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>建立及註冊以 COM 為基礎的自訂衝突解決器  
  
1.  在 COM 相容的撰寫環境中，加入對自訂衝突解決器程式庫的參考。  
  
2.  針對 Visual C++ 專案，使用 #import 指示詞將此程式庫匯入專案中。  
  
3.  建立可實作 **ICustomResolver** 介面的類別。  
  
4.  實作特定的方法和屬性。  
  
5.  建立專案來建立自訂衝突解決器程式庫檔案。  
  
6.  在包含合併代理程式可執行檔的目錄 (通常是 \Microsoft SQL Server\100\COM) 中部署此程式庫。  
  
    > [!NOTE]  
    >  如果是提取訂閱，則必須在訂閱者上部署自訂衝突解決器，如果是發送訂閱，則必須在散發者上部署，或是在搭配 Web 同步處理的 Web 伺服器上部署。  
  
7.  透過從部署目錄執行 regsvr32.exe 註冊自訂衝突解決器程式庫，如下面所示：  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)，以確認此程式庫尚未註冊為自訂衝突解析程式。  
  
9. 若要將此程式庫註冊為自訂衝突解析程式，請在散發者端執行 [sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)。 針對 **\@article_resolver** 指定 COM 物件的易記名稱，針對 **\@resolver_clsid** 指定程式庫的識別碼 (CLSID)，並為 **\@is_dotnet_assembly** 指定 **false** 值。  
  
    > [!NOTE]  
    >  當不再需要時，您可以透過使用 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) 來取消註冊自訂衝突解析程式。  
  
10. (選擇性) 在叢集上重複步驟 6-9，在此叢集的所有節點上註冊自訂解析程式。 要確定自訂解析程式可以在容錯移轉之後適當地載入重新調整器時，必須進行這些步驟。
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>搭配新的資料表發行項使用自訂衝突解決器  
  
1.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)，並記下所需解析程式的易記名稱。  
  
2.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 來定義發行項。 針對 **\@article_resolver** 指定步驟 1 中發行項解析程式的易記名稱。 如需詳細資訊，請參閱[定義發行項](../../relational-databases/replication/publish/define-an-article.md)。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>搭配現有的資料表發行項使用自訂衝突解決器  
  
1.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)，並記下所需解析程式的易記名稱。  
  
2.  執行 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)，針對 **\@property** 指定 **\@publication**、 **\@article**，以及 **article_resolver** 值，並為 **\@value** 指定步驟 1 中發行項解析程式的易記名稱。  
  

## <a name="see-also"></a>另請參閱  
 [進階合併複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [以 COM 為基礎的自訂解析程式](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
