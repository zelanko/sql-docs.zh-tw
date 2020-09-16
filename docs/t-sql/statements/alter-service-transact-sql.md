---
description: ALTER SERVICE (Transact-SQL)
title: ALTER SERVICE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SERVICE
- ALTER_SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- modifying services
- contracts [Service Broker], modifying
- ALTER SERVICE statement
- services [Service Broker], modifying
ms.assetid: 2b4608f7-bb2e-4246-aa29-b52c55995b3a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 08a4d8ad8ab23f1bfa618049462506c140090135
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547774"
---
# <a name="alter-service-transact-sql"></a>ALTER SERVICE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  變更現有的服務。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
ALTER SERVICE service_name   
   [ ON QUEUE [ schema_name . ]queue_name ]   
   [ ( < opt_arg > [ , ...n ] ) ]  
[ ; ]  
  
<opt_arg> ::=  
   ADD CONTRACT contract_name | DROP CONTRACT contract_name  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *service_name*  
 這是要變更的服務名稱。 您不可指定伺服器、資料庫和結構描述名稱。  
  
 ON QUEUE [ _schema_name_**.** ] *queue_name*  
 指定這項服務的新佇列。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會從目前的佇列中，將這項服務的所有訊息移到新佇列中。  
  
 ADD CONTRACT *contract_name*  
 指定要加入這項服務所顯示的合約集之合約。  
  
 DROP CONTRACT *contract_name*  
 指定要從這項服務所公開的合約集中刪除的合約。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會在針對與使用這份合約的這項服務的任何現有交談，傳送錯誤訊息。  
  
## <a name="remarks"></a>備註  
 當 ALTER SERVICE 陳述式刪除服務中的合約時，服務就不再是使用這份合約的交談目標。 因此，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 不會接受在這份合約上，指向這項服務的新交談。 使用這份合約的現有交談不會受到影響。  
  
 若要改變服務的 AUTHORIZATION，請使用 ALTER AUTHORIZATION 陳述式。  
  
## <a name="permissions"></a>權限  
 改變服務的權限預設為服務的擁有者、**db_ddladmin** 或 **db_owner** 固定資料庫角色的成員，以及 **sysadmin** 固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-queue-for-a-service"></a>A. 變更服務的佇列  
 下列範例會變更 `//Adventure-Works.com/Expenses` 服務，使其改用 `NewQueue` 佇列。  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE NewQueue ;  
```  
  
### <a name="b-adding-a-new-contract-to-the-service"></a>B. 將新合約加入服務中  
 下列範例會變更 `//Adventure-Works.com/Expenses` 服務，以允許 `//Adventure-Works.com/Expenses` 合約上的對話。  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="c-adding-a-new-contract-to-the-service-dropping-existing-contract"></a>C. 將新合約加入服務中，並卸除現有的合約  
 下列範例會變更 `//Adventure-Works.com/Expenses` 服務，以允許 `//Adventure-Works.com/Expenses/ExpenseProcessing` 合約上的對話，並禁止 `//Adventure-Works.com/Expenses/ExpenseSubmission` 合約上的對話。  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing],   
     DROP CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
