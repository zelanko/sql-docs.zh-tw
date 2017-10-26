---
title: "原始檔案自訂屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a364ae62ebc8823f9d57fb44ef99b7b14469c608
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="raw-file-custom-properties"></a>原始檔案自訂屬性
  **來源自訂屬性**  
  
 原始檔案來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是原始檔案來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|用來存取原始資料的模式。 可能的值為 [檔案名稱]\(0) 和 [來自變數的檔案名稱]\(1)。 預設值是 [檔案名稱]\(0)。|  
|FileName|字串|來源檔案的路徑和檔案名稱。|  
  
 原始檔案來源的輸出和輸出資料行沒有任何自訂屬性。  
  
 如需相關資訊，請參閱 [Raw File Source](../../integration-services/data-flow/raw-file-source.md)。  
  
 **目的地自訂屬性**  
  
 原始檔案目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是原始檔案目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|一個值，指定 FileName 屬性包含檔案名稱，或包含檔案名稱之變數的名稱。 選項為 [檔案名稱]\(0) 和 [來自變數的檔案名稱]\(1)。|  
|FileName|字串|原始檔案目的地寫入的檔案名稱。|  
|WriteOption|整數 (列舉)|一個值，指定原始檔案目的地是否會刪除具有相同名稱的現有檔案。 選項為 [永遠建立]\(0)、[建立一次]\(1)、[截斷與附加]\(3) 和 [附加]\(2)。 這個屬性的預設值是**永遠建立**(0)。|  
  
> [!NOTE]  
>  附加作業要求已附加資料的中繼資料與檔案中已有資料的中繼資料相符。  
  
 原始檔案目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需相關資訊，請參閱 [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  

