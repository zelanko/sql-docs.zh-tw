---
title: 執行 SQL 工作編輯器 （結果集頁面） |Microsoft 文件
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
- sql12.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: d27000c8-8d91-4e1c-b45e-bca9a3c12f6d
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b80d8052fd4492e0da04a65aa17e55f3e960d238
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135439"
---
# <a name="execute-sql-task-editor-result-set-page"></a>執行 SQL 工作編輯器 (結果集頁面)
  使用 [執行 SQL 工作編輯器] 對話方塊的 [結果集] 頁面，即可將 SQL 陳述式的結果對應至新的或現有的變數。 如果 [一般] 頁面上的 [結果集] 已設定為 [無]，就會停用此對話方塊中的選項。  
  
 如需這項工作的詳細資訊，請參閱[執行 SQL 工作](control-flow/execute-sql-task.md)和[執行 SQL 工作中的結果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)。  
  
## <a name="options"></a>選項。  
 **結果名稱**  
 按一下 [加入] 加入結果集對應集之後，請為結果提供名稱。 您必須根據結果集類型來使用特定的結果名稱。  
  
 如果結果集類型是「 **單一資料列**」，則您可以使用查詢所傳回之資料行的名稱，或查詢所傳回之資料行的資料行清單中，代表資料行位置的數字。  
  
 如果結果集類型為 **完整結果集** 或 **XML**，則必須使用 0 作為結果集名稱。  
  
 **相關主題**： [執行 SQL 工作中的結果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
 **變數名稱**  
 選取變數來將結果集對應至變數，或是按一下 [\<新增變數...>]，使用 [新增變數] 對話方塊來新增新的變數。  
  
 **[加入]**  
 按一下即可新增結果集對應。  
  
 **移除**  
 選取清單中的結果集對應，然後按一下 [移除]。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [執行 SQL 工作編輯器&#40;[一般] 頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [執行 SQL 工作編輯器&#40;參數對應頁面&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Transact-SQL 參考 &#40;Database Engine&#41;](/sql/t-sql/language-reference)  
  
  
