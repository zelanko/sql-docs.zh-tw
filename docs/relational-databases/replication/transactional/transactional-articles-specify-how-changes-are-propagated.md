---
title: 指定變更的傳播方式 (交易式)
description: 了解如何在 SQL Server 中指定交易式發行集變更的傳播方式。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
ms.assetid: a10c5001-22cc-4667-8f0b-3d0818dca2e9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: e7b267c0bfcfc7e12e2dc17c08bb6b18f2f36bf6
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "86919898"
---
# <a name="transactional-articles---specify-how-changes-are-propagated"></a>交易式發行項 - 指定變更的傳播方式
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  異動複寫可讓您指定資料變更從「發行者」傳播到「訂閱者」的方式。 對於每個發行的資料表，您都可以指定四種方法之一來傳播每個要傳播到「訂閱者」的作業 (INSERT、UPDATE 或 DELETE)：  
  
-   指定異動複寫應先編寫指令碼，然後呼叫預存程序，以將變更傳播至「訂閱者」(預設值)。  
  
-   指定變更使用 INSERT、UPDATE 或 DELETE 陳述式傳播 (非「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」的預設值)。  
  
-   指定使用自訂預存程序。  
  
-   指定不在任何「訂閱者」端執行此動作。 不會複寫該類型的交易。  
  
 依預設，異動複寫會透過每個訂閱者上所安裝的一組預存程序，將變更傳播到訂閱者。 在「發行者」端的資料表中進行插入、更新或刪除操作時，作業會翻譯為對「訂閱者」端預存程序的呼叫。 預存程序接受對應至資料表中資料行的參數，允許在「訂閱者」端變更這些資料行。  
  
 若要設定對交易式發行項之資料變更的傳播方法，請參閱＜ [設定對交易式發行項之資料變更的傳播方法](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)＞。  
  
## <a name="default-and-custom-stored-procedures"></a>預設與自訂預存程序  
 依預設，複寫為每個資料表發行項建立的三個程序為：  
  
-   **sp_MSins_\<** *tablename* **>** ，負責處理插入。  
  
-   **sp_MSupd_\<** *tablename* **>** ，負責處理更新。  
  
-   **sp_MSdel_\<** *tablename* **>** ，負責處理刪除。  
  
 程序中使用的 **\<**_tablename_**>** 取決於發行項新增至發行集的方式，以及訂閱資料庫是否包含擁有者不同的同名資料表。  
  
 以上任何程序均可取代為您在將發行項新增至發行集時指定的自訂程序。 如果應用程式需要自訂邏輯，例如在「訂閱者」端更新資料列時將資料插入稽核資料表，就要使用自訂程序。 如需指定自訂預存程序的詳細資訊，請參閱以上所列的「如何」主題。  
  
 如果指定預設複寫程序或自訂程序，則還要指定每個程序的呼叫語法 (如果使用預設程序，複寫會選取預設值)。 呼叫語法決定提供給程序的參數結構，以及每個資料變更傳送到「訂閱者」的資訊量。 如需詳細資訊，請參閱本主題中的「預存程序的呼叫語法」一節。  
  
### <a name="considerations-for-using-custom-stored-procedures"></a>使用自訂預存程序的考量  
 使用自訂預存程序時，請記住下列考量：  
  
-   您必須支援預存程序中的邏輯； [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 不支援自訂邏輯。  
  
-   為了避免與複寫使用的交易產生衝突，不應在自訂程序中使用外顯交易。  
  
-   「訂閱者」端的結構描述通常與「發行者」端的結構描述相同，但如果使用的是資料行篩選，則也可能是「發行者」結構描述的子集。 不過，如果需要在資料移動時轉換結構描述，好讓訂閱者上的結構描述不是發行者上結構描述的子集，建議採用 [!INCLUDE[ssISCurrent](../../../includes/ssiscurrent-md.md)] 方案。 如需詳細資訊，請參閱 [SQL Server Integration Services](../../../integration-services/sql-server-integration-services.md)。  
  
-   如果對發行的資料表進行了結構描述變更，則必須重新產生自訂程序。 如需詳細資訊，請參閱[重新產生自訂交易程序以反映結構描述變更](../../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)。  
  
-   如果「散發代理程式」的 **-SubscriptionStreams** 參數所使用的值大於 1，則必須確定主索引鍵資料行的更新成功。 例如：  
  
    ```  
    update ... set pk = 2 where pk = 1 -- update 1  
    update ... set pk = 3 where pk = 2 -- update 2  
    ```  
  
     如果「散發代理程式」使用多個連接，則可能會透過不同的連接複寫這兩個更新。 如果更新 1 先套用，便不會有問題；如果更新 2 先套用，則會傳回「0 個資料列受影響」，因為更新 1 尚未發生。 預設程序會對這種情況進行處理，如果沒有資料列受更新的影響，便會產生錯誤訊息：  
  
    ```  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sys.sp_MSreplraiserror 20598  
    ```  
  
     產生錯誤訊息將強制「散發代理程式」透過單一連接重試更新，這樣便會成功。 自訂預存程序必須包括類似的邏輯。  
  
### <a name="call-syntax-for-stored-procedures"></a>預存程序的呼叫語法  
 用於呼叫異動複寫所使用程序的語法有五個選項：  
  
-   CALL 語法。 可用於插入、更新與刪除。 依預設，複寫使用此語法進行插入和刪除。  
  
-   SCALL 語法。 僅能使用於更新。 依預設，複寫使用此語法進行更新。  
  
-   MCALL 語法。 僅能使用於更新。  
  
-   XCALL 語法。 可用於更新與刪除。  
  
-   VCALL。 用於可更新訂閱。 僅供內部使用。  
  
 每種方法傳播到「訂閱者」的資料量都不同。 例如，SCALL 僅傳遞實際受更新影響的資料行值。 相反地，XCALL 則要求所有資料行 (無論是否受更新影響) 以及每個資料行的所有舊資料值。 在許多情況下，SCALL 適用於更新，但如果您的複寫在更新過程中要求所有資料值，則 XCALL 適用。  
  
#### <a name="call-syntax"></a>CALL 語法  
 INSERT 預存程序  
 處理 INSERT 陳述式的預存程序將會收到所有資料行之插入值：  
  
```  
c1, c2, c3,... cn  
```  
  
 UPDATE 預存程序  
 處理 UPDATE 陳述式的預存程序將會收到在發行項中定義的所有資料行之更新值，接著是主索引鍵資料行的原始值 (不會嘗試判斷哪些資料行作了變更)：  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn  
```  
  
 DELETE 預存程序  
 處理 DELETE 陳述式的預存程序會收到主索引鍵資料行的值：  
  
```  
pkc1, pkc2, pkc3,... pkcn  
```  
  
#### <a name="scall-syntax"></a>SCALL 語法  
 UPDATE 預存程序  
 處理 UPDATE 陳述式的預存程序會只收到那些已變更資料行的更新值，接著是主索引鍵資料行的原始值，然後是指出已變更資料行的位元遮罩 (**binary(n)** ) 參數。 在下列範例中，資料行 2 (c2) 未變更：  
  
```  
c1, , c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="mcall-syntax"></a>MCALL 語法  
 UPDATE 預存程序  
 處理 UPDATE 陳述式的預存程序會收到發行項中所定義的所有資料行之更新值，接著是主索引鍵資料行的原始值，然後是指出已變更資料行的位元遮罩 (**binary(n)** ) 參數：  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="xcall-syntax"></a>XCALL 語法  
 UPDATE 預存程序  
 處理 UPDATE 陳述式的預存程序會收到發行項中所定義的所有資料行之原始值 (前置資料影像)，接著是發行項中定義的所有資料行之更新值 (後置資料影像)：  
  
```  
old-c1, old-c2, old-c3,... old-cn, c1, c2, c3,... cn,  
```  
  
 DELETE 預存程序  
 處理 DELETE 陳述式的預存程序會收到發行項中定義的所有資料行之原始值 (前置資料影像)：  
  
```  
old-c1, old-c2, old-c3,... old-cn  
```  
  
> [!NOTE]  
>  使用 XCALL 時， **text** 與 **image** 資料行的前置資料影像值預期為 NULL。  
  
## <a name="examples"></a>範例  
 下列程序是為 `Vendor Table` 範例資料庫中的 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] 建立的預設程序。  
  
```  
--INSERT procedure using CALL syntax  
create procedure [sp_MSins_PurchasingVendor]   
  @c1 int,@c2 nvarchar(15),@c3 nvarchar(50),@c4 tinyint,@c5 bit,@c6 bit,@c7 nvarchar(1024),@c8 datetime  
as   
begin   
insert into [Purchasing].[Vendor]([VendorID]  
,[AccountNumber]  
,[Name]  
,[CreditRating]  
,[PreferredVendorStatus]  
,[ActiveFlag]  
,[PurchasingWebServiceURL]  
,[ModifiedDate])  
values (   
 @c1  
,@c2  
,@c3  
,@c4  
,@c5  
,@c6  
,@c7  
,@c8  
 )   
end  
go  
  
--UPDATE procedure using SCALL syntax  
create procedure [sp_MSupd_PurchasingVendor]   
 @c1 int = null,@c2 nvarchar(15) = null,@c3 nvarchar(50) = null,@c4 tinyint = null,@c5 bit = null,@c6 bit = null,@c7 nvarchar(1024) = null,@c8 datetime = null,@pkc1 int  
,@bitmap binary(2)  
as  
begin  
update [Purchasing].[Vendor] set   
 [AccountNumber] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [AccountNumber] end  
,[Name] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [Name] end  
,[CreditRating] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [CreditRating] end  
,[PreferredVendorStatus] = case substring(@bitmap,1,1) & 16 when 16 then @c5 else [PreferredVendorStatus] end  
,[ActiveFlag] = case substring(@bitmap,1,1) & 32 when 32 then @c6 else [ActiveFlag] end  
,[PurchasingWebServiceURL] = case substring(@bitmap,1,1) & 64 when 64 then @c7 else [PurchasingWebServiceURL] end  
,[ModifiedDate] = case substring(@bitmap,1,1) & 128 when 128 then @c8 else [ModifiedDate] end  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end  
go  
  
--DELETE procedure using CALL syntax  
create procedure [sp_MSdel_PurchasingVendor]   
  @pkc1 int  
as   
begin   
delete [Purchasing].[Vendor]  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end   
go  
```  
  
## <a name="see-also"></a>另請參閱  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
