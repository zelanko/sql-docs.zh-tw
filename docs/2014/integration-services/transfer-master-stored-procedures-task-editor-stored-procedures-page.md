---
title: 傳送主要預存程式工作編輯器（預存程式頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: 5fcf171e-cc0b-4c24-8eb5-3a4b4775e64a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0cd0b269c0ced445017d573cfad08a767d5f2008
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439985"
---
# <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>傳送主要預存程序工作編輯器 (預存程序頁面)
  使用 [傳送主要預存程序工作編輯器]**** 對話方塊的 [預存程序]**** 頁面，即可指定屬性，以將一個或多個使用者定義預存程序從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體之某個執行個體的 **master** 資料庫，複製到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之另一個執行個體的 **master** 資料庫中。 如需這項工作的詳細資訊，請參閱 [傳送主要預存程序工作](control-flow/transfer-master-stored-procedures-task.md)。  
  
> [!NOTE]  
>  此工作只會從來源伺服器上的 **master** 資料庫，將 **dbo** 擁有的使用者定義預存程序，傳送到目的地伺服器上的 **master** 資料庫。 使用者必須有目的地伺服器上之 **master** 資料庫的 CREATE PROCEDURE 權限，或是目的地伺服器上之 **sysadmin** 固定伺服器角色的成員，才能在目的地伺服器建立預存程序。  
  
## <a name="options"></a>選項  
 **SourceConnection**  
 在清單中選取 SMO 連線管理員，或按一下 **\<New connection...>** 以建立與來源伺服器的新連接。  
  
 **[Destinationconnection**  
 在清單中選取 SMO 連線管理員，或按一下 **\<New connection...>** 以建立目的地伺服器的新連接。  
  
 **IfObjectExists**  
 選取工作應如何處理在目的地伺服器上的 **master** 資料庫中已經存在有相同名稱的使用者定義預存程序。  
  
 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**FailTask**|如果目的地伺服器上的 **master** 資料庫中已經存在有相同名稱的預存程序，則工作失敗。|  
|**Overwrite**|工作會覆寫目的地伺服器上的 **master** 資料庫中有相同名稱的預存程序。|  
|**略過**|工作會略過目的地伺服器上的 **master** 資料庫中存在有相同名稱的預存程序。|  
  
 **TransferAllStoredProcedures**  
 選取是否應將來源伺服器上之 **master** 資料庫中的所有使用者定義預存程序，複製到目的地伺服器。  
  
|值|描述|  
|-----------|-----------------|  
|**True**|複製 **master** 資料庫中的所有使用者定義預存程序。|  
|**False**|只複製指定的預存程序。|  
  
 **StoredProceduresList**  
 選取應將來源伺服器上之 **master** 資料庫中的哪些使用者定義預存程序，複製到目的地 **master** 資料庫。 只有 [TransferAllStoredProcedures]**** 設定為 [False]**** 時，才能使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [傳送主要預存程式工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [SMO 連線管理員](connection-manager/smo-connection-manager.md)  
  
  
