---
title: "大量插入工作編輯器 （選項頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: b3702811-3eb8-4b28-9190-5ae7a1a7bb6f
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1a714027caa6581a56d9f22da84c48d469e80cb1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="bulk-insert-task-editor-options-page"></a>大量插入工作編輯器 (選項頁面)
  使用 **[大量插入工作編輯器]** 對話方塊的 **[選項]** 頁面，即可設定大量插入作業的屬性。 大量插入工作會將大量資料複製至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或檢視表。  
  
 若要了解如何使用大量插入，請參閱[大量插入工作](../../integration-services/control-flow/bulk-insert-task.md)和 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)。  
  
## <a name="options"></a>選項。  
 **CodePage**  
 指定資料檔中之資料的字碼頁。  
  
 **DataFileType**  
 指定載入作業所用的資料類型值。  
  
 **BatchSize**  
 指定批次中的資料列數目。 預設為整個資料檔。 如果您將 **[BatchSize]** 設定為零，則會以單一批次載入資料。  
  
 **LastRow**  
 指定要複製的最後一個資料列。  
  
 **FirstRow**  
 指定要開始複製的第一個資料列。  
  
 **[大量插入工作編輯器]**  
 |詞彙|定義|  
|----------|----------------|  
|**檢查條件約束**|選取此選項可檢查資料表與資料行條件約束。|  
|**保留 Null**|選取此選項可在大量插入作業期間保留 Null 值，而不是在空白資料行插入任何預設值。|  
|**啟用識別插入**|選取此選項可將現有的值插入識別欄位。|  
|**資料表鎖定**|選取此選項可在大量插入期間鎖定資料表。|  
|**引發觸發程序**|選取即可引發資料表上的任何插入、更新或刪除觸發程序。|  
  
 **SortedData**  
 在大量插入陳述式中指定 ORDER BY 子句。 您所提供的資料行名稱必須是目的資料表中的有效資料行。 預設值為 **false**。 這表示資料並未依 ORDER BY 子句排序。  
  
 **MaxErrors**  
 指定取消大量插入作業之前，可以發生的錯誤數目上限。 值為 0 指出允許發生無限個錯誤。  
  
> [!NOTE]  
>  大量載入作業無法匯入的每個資料列都會計算為一個錯誤。  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [大量插入工作編輯器 &#40;一般頁面 &#41;](../../integration-services/control-flow/bulk-insert-task-editor-general-page.md)   
 [大量插入工作編輯器 &#40;連接頁面 &#41;](../../integration-services/control-flow/bulk-insert-task-editor-connection-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
