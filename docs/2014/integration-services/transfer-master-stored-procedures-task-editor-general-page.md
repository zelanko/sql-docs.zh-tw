---
title: 傳送主要預存程序工作編輯器 （一般頁面） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.transferstoredprocedurestask.general.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: fa1abd4c-e2be-427f-be53-860e49c97227
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 624b1fca90b4d5fd92ef557dea561539ac8ba6e6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037263"
---
# <a name="transfer-master-stored-procedures-task-editor-general-page"></a>傳送主要預存程序工作編輯器 (一般頁面)
  使用 [傳送主要預存程序工作編輯器] 對話方塊的 [一般] 頁面，即可命名和描述傳送主要預存程序工作。 如需這項工作的詳細資訊，請參閱[傳送主要預存程序工作](control-flow/transfer-master-stored-procedures-task.md)。  
  
> [!NOTE]  
>  此工作只會從來源伺服器上的 **master** 資料庫，將 **dbo** 擁有的使用者定義預存程序，傳送到目的地伺服器上的 **master** 資料庫。 使用者必須有目的地伺服器上之 **master** 資料庫的 CREATE PROCEDURE 權限，或是目的地伺服器上之 **sysadmin** 固定伺服器角色的成員，才能在目的地伺服器建立預存程序。  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入傳送主要預存程序工作的唯一名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入傳送主要預存程序工作的描述。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [傳送主要預存程序工作編輯器 &#40;預存程序頁面&#41;](../../2014/integration-services/transfer-master-stored-procedures-task-editor-stored-procedures-page.md)   
 [運算式頁面](expressions/expressions-page.md)  
  
  