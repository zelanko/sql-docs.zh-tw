---
title: "來源資料庫檔案 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
ms.assetid: 7dc6bfeb-37c1-45e8-a705-a87564922265
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0fb66420c0073a79ba6b78608de09fd901c738c0
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="source-database-files"></a>來源資料庫檔案
  使用 **[來源資料庫檔案]** 對話方塊，即可檢視來源伺服器上的資料庫檔案名稱和位置，或指定傳送資料庫工作的網路檔案共用位置。 如需這項工作的詳細資訊，請參閱 [傳送資料庫工作](../../integration-services/control-flow/transfer-database-task.md)。  
  
 若要以來源伺服器上的資料庫檔案名稱和位置來擴展此對話方塊，請在 **[傳送資料庫工作編輯器]** 對話方塊的 **[資料庫]** 頁面中，首先指定 **[SourceConnection]** 和 **[SourceDatabaseName]** 。  
  
## <a name="options"></a>選項。  
 **來源檔案**  
 在來源伺服器上，將會被傳送的資料庫檔案名稱。 **[來源檔案]** 是唯讀的。  
  
 **來源資料夾**  
 在來源伺服器上，要傳送之資料庫檔案所在的資料夾。 **[來源資料夾]** 是唯讀的。  
  
 **網路檔案共用**  
 在來源伺服器上，會從中傳送資料庫檔案的網路共用資料夾。 當您在 **[傳送資料庫工作編輯器]** 對話方塊的 **[資料庫]** 頁面中，將 **[方法]** 指定為 **[DatabaseOffline]** ，以離線模式傳送資料庫時，請使用 **[網路檔案共用]** 。  
  
 輸入網路檔案共用位置，或按一下 [瀏覽 (…)] 按鈕以尋找網路檔案共用位置。  
  
 在離線模式中傳送資料庫時，資料庫檔案會複製到來源伺服器上的 **[網路檔案共用]** 位置之後，才傳送到目的地伺服器。  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [傳送資料庫工作編輯器 &#40;一般頁面 &#41;](../../integration-services/control-flow/transfer-database-task-editor-general-page.md)   
 [傳送資料庫工作編輯器 &#40; 資料庫頁面 &#41;](../../integration-services/control-flow/transfer-database-task-editor-databases-page.md)  
  
  
