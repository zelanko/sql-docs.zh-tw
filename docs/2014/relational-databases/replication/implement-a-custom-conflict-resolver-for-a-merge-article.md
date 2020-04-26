---
title: 針對合併發行項實作自訂衝突解析程式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 47d0f7c4eb6c78b9e551fafdc1e018a27604086e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721234"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>針對合併發行項實作自訂衝突解析程式
   本主題描述如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或[以 COM 為基礎的自訂解析程式](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中針對合併發行項實作自訂衝突解析程式。  
  
 **本主題內容**  
  
-   **若要針對合併發行項實作自訂衝突解析程式，請使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [以 COM 為基礎的解析程式](#COM)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以將自訂衝突解決器撰寫為每一個發行者上的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序。 在同步處理期間，當註冊解決器的發行項中遇到衝突時，就會叫用此預存程序，而且衝突資料列的相關資訊會由合併代理程式傳遞給此程序所需的參數。 一定會在發行者上建立以預存程序為基礎的自訂衝突解決器。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預存程式解析程式的叫用目的，只是為了處理資料列變更為基礎的衝突。 這些解決器不能用於處理其他類型的衝突，例如因為 PRIMARY KEY 違規或唯一索引條件約束違規而發生的插入失敗。  
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>建立以預存程序為基礎的自訂衝突解決器  
  
1.  在發行集或 **msdb** 資料庫的發行者上，建立新的系統預存程序，以實作下列必要的參數：  
  
    |參數|資料類型|描述|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|`sysname`|解決衝突所針對之資料表的擁有者名稱。 這是發行集資料庫中資料表的擁有者。|  
    |**@tablename**|`sysname`|解決衝突所針對之資料表的名稱。|  
    |**@rowguid**|`uniqueidentifier`|發生衝突之資料列的唯一識別碼。|  
    |**@subscriber**|`sysname`|傳播衝突變更所在的伺服器名稱。|  
    |**@subscriber_db**|`sysname`|傳播衝突變更所在的資料庫名稱。|  
    |**@log_conflict輸出**|`int`|合併處理是否應該記錄衝突供稍後解決之用：<br /><br /> **0** = 不記錄衝突。<br /><br /> **1** = 訂閱者為衝突失敗者。<br /><br /> **2** = 發行者為衝突失敗者。|  
    |**@conflict_message輸出**|`nvarchar(512)`|當記錄衝突時，要提供之有關解決方法的訊息。|  
    |**@destowner**|`sysname`|訂閱者上發行之資料表的擁有者。|  
  
     此預存程序會使用由合併代理程式傳遞給這些參數的值，以實作自訂衝突解決邏輯；它必須傳回結構上與基底資料表相同的單一資料列結果集，並包含此資料列之獲勝版本的資料值。  
  
2.  將預存程序的 EXECUTE 權限授與給訂閱者使用的任何登入，以連接到發行者。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>搭配新的資料表發行項使用自訂衝突解決器  
  
1.  執行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 來定義發行項，針對 **@article_resolver** **參數指定** Microsoft SQL **@article_resolver** 的值，並針對 **@resolver_info** 參數指定可實作衝突解決器邏輯的預存程序名稱。 如需詳細資訊，請參閱 [定義發行項](publish/define-an-article.md)。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>搭配現有的資料表發行項使用自訂衝突解決器  
  
1.  執行[sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)，並**@publication**指定**@article**、、的**article_resolver** **@property**值，以及**@value**為**MicrosoftSQL** **伺服器儲存的 ProcedureResolver**值。  
  
2.  執行[sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)，並**@publication**指定**@article**、、 **resolver_info**的**@property**值，以及為執行衝突解決器邏輯的預存程式名稱**@value**。  
  
##  <a name="using-a-com-based-custom-resolver"></a><a name="COM"></a>使用以 COM 為基礎的自訂解析程式  
 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 命名空間會實作一個介面，此介面可讓您撰寫複雜的商務邏輯來處理事件，並解決合併複寫同步處理程序期間所發生的衝突。 如需詳細資訊，請參閱 [為合併發行項實作商務邏輯處理常式](implement-a-business-logic-handler-for-a-merge-article.md)。 您也可以撰寫自己的原生程式碼式自訂商務邏輯，以解決衝突。 此邏輯會建立為 COM 元件，並編譯成動態連結程式庫 (DLL) (使用類似 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++ 的產品)。 這類以 COM 為基礎的自訂衝突解決器必須實**ICustomResolver**介面，這是特別針對衝突解決所設計。  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>建立及註冊以 COM 為基礎的自訂衝突解決器  
  
1.  在 COM 相容的撰寫環境中，加入對自訂衝突解決器程式庫的參考。  
  
2.  針對 Visual C++ 專案，使用 #import 指示詞將此程式庫匯入專案中。  
  
3.  建立可實作 **ICustomResolver** 介面的類別。  
  
4.  實作特定的方法和屬性。  
  
5.  建立專案來建立自訂衝突解決器程式庫檔案。  
  
6.  在包含合併代理程式可執行檔的目錄中 (通常是 \Microsoft SQL Server\100\COM) 部署此程式庫。  
  
    > [!NOTE]  
    >  如果是提取訂閱，則必須在訂閱者上部署自訂衝突解決器，如果是發送訂閱，則必須在散發者上部署，或是在搭配 Web 同步處理的 Web 伺服器上部署。  
  
7.  從部署目錄使用 regsvr32.exe 註冊自訂衝突解決器程式庫，如下面所示：  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)，以確認此程式庫尚未註冊為自訂衝突解決器。  
  
9. 若要將程式庫註冊為自訂衝突解決器，請在「散發者」[端執行 &#40;transact-sql&#41;sp_registercustomresolver ](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql)。 針對**@article_resolver**指定 COM 物件的易記名稱、針對指定程式庫的識別碼（CLSID） **@resolver_clsid**，並`false`針對**@is_dotnet_assembly**[值]。  
  
    > [!NOTE]  
    >  當不再需要時，可以使用 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql) 來取消註冊自訂衝突解決器。  
  
10. (選擇性) 在叢集上重複步驟 5-8，在此叢集的所有節點上註冊自訂解決器。 要確定自訂解決器將能夠在容錯移轉之後適當地載入重新調整器時，必須進行這項處理。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>搭配新的資料表發行項使用自訂衝突解決器  
  
1.  在發行者上，執行[sp_enumcustomresolvers &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)並記下所需解析程式的易記名稱。  
  
2.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 來定義發行項。 針對**@article_resolver**指定步驟1中發行項解析程式的易記名稱。 如需詳細資訊，請參閱 [定義發行項](publish/define-an-article.md)。  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>搭配現有的資料表發行項使用自訂衝突解決器  
  
1.  在發行者上，執行[sp_enumcustomresolvers &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)並記下所需解析程式的易記名稱。  
  
2.  執行[sp_changemergearticle &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)、 **@publication**指定、 **@article**、的**article_resolver**值**@property**，以及步驟1中發行項解析程式的易記名稱。 **@value**  
  
#### <a name="viewing-a-sample-custom-resolver"></a>檢視自訂解析程式範例  
  
1.  SQL Server 2000 範例檔案中有提供範例。 下載[**sql2000samples.cab**](https://github.com/Microsoft/sql-server-samples/blob/master/samples/tutorials/Miscellaneous/sql2000samples.zip)。 這會將3個檔案 amounting 下載到 6.9 MB。  
  
2.  從下載的 .cab 壓縮檔解壓縮檔案。  
  
3.  執行**setup.exe**  
  
    > [!NOTE]  
    >  選擇安裝選項時，只需要安裝 **複寫** 範例。 （預設安裝路徑為**C:\Program Files （x86） \Microsoft SQL Server 2000 Samples\1033\\**）  
  
4.  移至安裝資料夾。 (預設資料夾是 **C:\Program Files (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**)  
  
5.  執行 **unzip_sqlreplSP3.exe** 程式。  
  
    > [!NOTE]  
    >  範例 COM 解析程式將會安裝至 **C:\Program Files (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** 資料夾 (預設值)。  
  
6.  在 **subspres** 資料夾中，於所有來源檔案中尋找 **#include sqlres.h** ，並將其取代為 **#import "replrec.dll" no_namespace, raw_interfaces_only**  
  
## <a name="see-also"></a>另請參閱  
 [先進合併式複寫衝突偵測與解決](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [以 COM 為基礎的自訂解析程式](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [複寫安全性最佳作法](security/replication-security-best-practices.md)  
  
  
