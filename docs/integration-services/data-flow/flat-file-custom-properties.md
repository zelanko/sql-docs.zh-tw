---
title: "一般檔案自訂屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 097c9a07d738bb1b192095ac91448487fdfa0eb1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="flat-file-custom-properties"></a>一般檔案自訂屬性
  **來源自訂屬性**  
  
 一般檔案來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是一般檔案來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|字串|包含檔案名稱之輸出資料行的名稱。 如果沒有指定任何名稱，就不會產生包含檔案名稱的輸出資料行。<br /><br /> 注意：雖然您無法在 [一般檔案來源編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|RetainNulls|布林|一個值，指定當「資料轉換管線」引擎處理資料時，是否要將來源檔案的 Null 值保留成 Null 值。 此屬性的預設值為 **False**。|  
  
 一般檔案來源的輸出沒有任何自訂屬性。  
  
 下表描述的是一般檔案來源之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|FastParse|布林|一個值，指出資料行會使用 DTS 所提供之速度更快但不區分地區設定的快速剖析常式，還是區分地區設定的標準剖析常式。 如需詳細資訊，請參閱 [快速剖析](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 和 [標準剖析](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)。 此屬性的預設值為 **False**。<br /><br /> 注意：雖然您無法在 [一般檔案來源編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
  
 如需詳細資訊，請參閱 [一般檔案來源](../../integration-services/data-flow/flat-file-source.md)。  
  
 **目的地自訂屬性**  
  
 一般檔案目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是一般檔案目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|標頭|字串|寫入任何資料之前插入檔案中的文字區塊。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
|Overwrite|布林|一個值，指定要覆寫或附加至具有相同名稱的現有目的地檔案。 此屬性的預設值為 [True]。|  
  
 一般檔案目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [一般檔案目的地](../../integration-services/data-flow/flat-file-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  

