---
title: "ALTER BROKER PRIORITY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_BROKER_TSQL
- ALTER BROKER PRIORITY
- ALTER BROKER
- ALTER_BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER BROKER PRIORITY statement
- ssbdiagnose
ms.assetid: 15fda1b2-e4dd-4f9d-935a-2e38926075b2
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ad652e17039cbb6a6936b074320096fd58a78d3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-broker-priority-transact-sql"></a>ALTER BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 交談優先權的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
{ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = { PriorityValue | DEFAULT } ]  
              )  
}  
[;]  
  
```  
  
## <a name="arguments"></a>引數  
 *ConversationPriorityName*  
 指定要變更的交談優先權名稱。 此名稱必須參考目前資料庫中的交談優先權。  
  
 SET  
 指定用來判斷交談優先權是否套用到交談的準則。 SET 為必要項目，而且至少必須包含一個準則：CONTRACT_NAME、LOCAL_SERVICE_NAME、REMOTE_SERVICE_NAME 或 PRIORITY_LEVEL。  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 指定合約名稱，以用來做為判斷交談優先權是否要套用到交談的準則。 *ContractName*是[!INCLUDE[ssDE](../../includes/ssde-md.md)]識別碼，而且必須在目前資料庫中指定的合約名稱。  
  
 *ContractName*  
 指定交談優先權可以套用到交談，其中起始交談的 BEGIN DIALOG 陳述式指定 ON CONTRACT *ContractName*。  
  
 ANY  
 指定交談優先權可以套用到任何交談，不論它使用哪一個合約。  
  
 如果未指定 CONTRACT_NAME，則此交談優先權的合約屬性將不會變更。  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 指定用來判斷交談優先權是否套用到交談端點之準則的服務名稱。  
  
 *LocalServiceName*是[!INCLUDE[ssDE](../../includes/ssde-md.md)]識別項和必須在目前資料庫中指定的服務名稱。  
  
 *LocalServiceName*  
 指定交談優先權可以套用到以下項目：  
  
-   起始端服務名稱符合任何起始端交談端點*LocalServiceName*。  
  
-   目標服務名稱符合任何目標交談端點*LocalServiceName*。  
  
 ANY  
 -   指定交談優先權可以套用到任何交談端點，不論此端點使用的本機服務名稱為何。  
  
 如果未指定 LOCAL_SERVICE_NAME，則此交談優先權的本機服務屬性將不會變更。  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' |**ANY**}  
 指定用來判斷交談優先權是否套用到交談端點之準則的服務名稱。  
  
 *RemoteServiceName*是類型的常值**nvarchar （256)**。 [!INCLUDE[ssSB](../../includes/sssb-md.md)]使用位元組的比較，以比對*RemoteServiceName*字串。 這項比較會區分大小寫，且不會考慮目前的定序。 目標服務可以在目前的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體或遠端 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中。  
  
 '*RemoteServiceName*'  
 指定交談優先權可以指派到以下項目：  
  
-   任何起始端交談端點相關聯的目標服務名稱符合*RemoteServiceName*。  
  
-   任何目標交談端點相關聯的起始端服務名稱符合*RemoteServiceName*。  
  
 ANY  
 指定交談優先權會套用到任何交談端點，不論與此端點有關的遠端服務名稱為何。  
  
 如果未指定 REMOTE_SERVICE_NAME，則此交談優先權的遠端服務屬性將不會變更。  
  
 PRIORITY_LEVEL = { *PriorityValue* | **預設**}  
 指定優先權等級，以指派使用交談優先權中指定之合約和服務的任何交談端點。 *PriorityValue*必須是從 1 （最低優先權） 到 10 （最高優先權） 常值的整數。  
  
 如果未指定 PRIORITY_LEVEL，則此交談優先權的優先權等級屬性將不會變更。  
  
## <a name="remarks"></a>備註  
 ALTER BROKER PRIORITY 所變更的任何屬性都不會套用到現有的交談。 現有的交談會繼續使用在啟動時所指派的優先權。  
  
 如需詳細資訊，請參閱[CREATE BROKER PRIORITY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 預設值的成員建立交談優先權的權限**db_ddladmin**或**db_owner**固定資料庫角色以及**sysadmin**固定的伺服器角色。 需要資料庫的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-only-the-priority-level-of-an-existing-conversation-priority"></a>A. 只變更現有交談優先權的優先權等級。  
 變更優先權等級，但是不變更合約、本機服務或遠端服務的屬性。  
  
```  
ALTER BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-changing-all-of-the-properties-of-an-existing-conversation-priority"></a>B. 變更現有交談優先權的所有屬性。  
 變更優先權層級、合約、本機服務和遠端服務的屬性。  
  
```  
ALTER BROKER PRIORITY SimpleContractPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContractB,  
         LOCAL_SERVICE_NAME = TargetServiceB,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceB',  
         PRIORITY_LEVEL = 8);  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立 BROKER 優先權 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys.conversation_priorities &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
