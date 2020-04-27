---
title: ADO NET 自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e062a9ab-1e6b-4061-845a-4f8a0552b09d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ee7d1aba2b468c8aa0420bbacc76aea652ae7556
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62828662"
---
# <a name="ado-net-custom-properties"></a>ADO NET 自訂屬性
  **來源自訂屬性**  
  
 ADO NET 來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表將描述 ADO NET 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|CommandTimeout|String|一個值，指定 SQL 命令逾時之前的秒數。值為 0 表示此命令永遠不會逾時。|  
|SqlCommand|String|ADO NET 來源用來擷取資料的 SQL 陳述式。<br /><br /> 載入封裝時，您可以使用 ADO NET 來源即將使用的 SQL 陳述式，以動態方式更新此屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../expressions/integration-services-ssis-expressions.md)和[在封裝中使用屬性運算式](../expressions/use-property-expressions-in-packages.md)。|  
|AllowImplicitStringConversion|Boolean|指出是否會發生下列情況的值：<br /><br /> 如果外部中繼資料類型與屬於字串 (DT_WSTR 或 DT_NTEXT) 的輸出資料行類型之間具有不符項目，就不會產生驗證錯誤。<br /><br /> 將外部中繼資料類型隱含轉換成輸出資料行所使用的字串資料類型。<br /><br /> <br /><br /> 預設值為 TRUE。<br /><br /> 如需詳細資訊，請參閱 [ADO NET 來源](ado-net-source.md)。|  
  
 ADO NET 來源的輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [ADO NET 來源](ado-net-source.md)。  
  
 **目的地自訂屬性**  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目的地同時具有自訂屬性，以及所有資料流程元件通用的屬性。  
  
 下表描述 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 目的地的自訂屬性。 所有屬性都是可讀寫的。 雖然您無法在 [ADO NET 目的地編輯器]  中使用這些屬性，但是可以使用 [進階編輯器]  來設定這些屬性。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|BatchSize|整數|傳送給伺服器之批次內的資料列數。 值為 **0** 表示批次大小與內部緩衝區大小相符。 這個屬性的預設值為 **0**。|  
|CommandTimeout|整數|逾時之前 SQL 命令可以執行的秒數上限。值為 **0** 指出無限的時間。 這個屬性的預設值為 **0**。|  
|TableOrViewName|String|目的地資料表或檢視的名稱。|  
  
 如需詳細資訊，請參閱 [ADO NET 目的地](ado-net-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  
