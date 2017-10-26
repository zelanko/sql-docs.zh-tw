---
title: "ADO NET 自訂屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e062a9ab-1e6b-4061-845a-4f8a0552b09d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e16ce0117e36cfd15f8f1cde1bb8c7ce9ac2df55
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="ado-net-custom-properties"></a>ADO NET 自訂屬性
  **來源自訂屬性**  
  
 ADO NET 來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表將描述 ADO NET 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|CommandTimeout|字串|一個值，指定 SQL 命令逾時之前的秒數。值為 0 表示此命令永遠不會逾時。|  
|SqlCommand|字串|ADO NET 來源用來擷取資料的 SQL 陳述式。<br /><br /> 載入封裝時，您可以使用 ADO NET 來源即將使用的 SQL 陳述式，以動態方式更新此屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)和[在封裝中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)。|  
|AllowImplicitStringConversion|布林|指出是否會發生下列情況的值：<br /><br /> -如果外部中繼資料類型與屬於字串 (DT_WSTR 或 DT_NTEXT) 的輸出資料行類型之間具有不符項目，就不會產生驗證錯誤。<br /><br /> -將外部中繼資料類型隱含轉換成輸出資料行所使用的字串資料類型。<br /><br /> <br /><br /> 預設值為 TRUE。<br /><br /> 如需詳細資訊，請參閱 [ADO NET 來源](../../integration-services/data-flow/ado-net-source.md)。|  
  
 ADO NET 來源的輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [ADO NET 來源](../../integration-services/data-flow/ado-net-source.md)。  
  
 **目的地自訂屬性**  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目的地同時具有自訂屬性，以及所有資料流程元件通用的屬性。  
  
 下表描述 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目的地的自訂屬性。 所有屬性都是可讀寫的。 雖然您無法在 [ADO NET 目的地編輯器] 中使用這些屬性，但是可以使用 [進階編輯器] 來設定這些屬性。  
  
|屬性|資料類型|說明|  
|--------------|---------------|-----------------|  
|BatchSize|Integer|傳送給伺服器之批次內的資料列數。 值為 **0** 表示批次大小與內部緩衝區大小相符。 這個屬性的預設值為 **0**。|  
|CommandTimeout|Integer|逾時之前 SQL 命令可以執行的秒數上限。值為 **0** 指出無限的時間。 這個屬性的預設值為 **0**。|  
|TableOrViewName|字串|目的地資料表或檢視的名稱。|  
  
 如需詳細資訊，請參閱 [ADO NET 目的地](../../integration-services/data-flow/ado-net-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  

