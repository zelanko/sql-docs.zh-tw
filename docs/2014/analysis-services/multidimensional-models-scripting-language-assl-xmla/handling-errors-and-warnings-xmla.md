---
title: 處理錯誤和警告 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- inline errors [XMLA]
- SOAP faults [XML for Analysis]
- XML for Analysis, errors
- faults [XML for Analysis]
- messages [XML for Analysis]
- XMLA, errors
- warnings [XML for Analysis]
- inline warnings [XMLA]
ms.assetid: ab895282-098d-468e-9460-032598961f45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a41e9cedf8a2a19aea0cf8a374bc71f520ff52f
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147743"
---
# <a name="handling-errors-and-warnings-xmla"></a>處理錯誤和警告 (XMLA)
  當 XML for Analysis (XMLA) 時，就需要錯誤處理[Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)或是[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法呼叫未執行、 成功執行但產生錯誤或是警告，或成功執行但傳回的結果包含錯誤。  
  
|錯誤|報告|  
|-----------|---------------|  
|XMLA 方法呼叫未執行|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 傳回 SOAP 錯誤訊息包含失敗的詳細資料。<br /><br /> 如需詳細資訊，請參閱 區段中，[處理 SOAP 錯誤](#handling_soap_faults)。|  
|方法呼叫成功時的錯誤或警告|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含[錯誤](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla)或是[警告](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla)項目，針對每個錯誤或警告，分別在[訊息](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)屬性[根](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla)項目包含方法呼叫的結果。<br /><br /> 如需詳細資訊，請參閱 區段中，[處理錯誤和警告](#handling_errors_and_warnings)。|  
|方法呼叫成功時結果中的錯誤|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含內嵌`error`或`warning`錯誤或警告，項目分別內適當[資料格](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)或[列](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla)之結果的方法呼叫的項目。<br /><br /> 如需詳細資訊，請參閱 區段中，[處理內嵌錯誤和警告](#handling_inline_errors_and_warnings)。|  
  
##  <a name="handling_soap_faults"></a> 處理 SOAP 錯誤  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在發生下列情況時會傳回 SOAP 錯誤：  
  
-   包含 XMLA 方法的 SOAP 訊息，其格式不正確或是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體無法驗證它。  
  
-   發生通訊錯誤或是其他有關包含 XMLA 方法之 SOAP 訊息的錯誤。  
  
-   XMLA 方法並未在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上執行。  
  
 以 "XMLForAnalysis" 開頭的 XMLstartA 之 SOAP 錯誤碼，後面會接著句號和十六進位的 HRESULT 結果碼。 例如，`0x80000005` 的錯誤碼會格式化為 "`XMLForAnalysis.0x80000005`"。 如需有關 SOAP 錯誤格式的詳細資訊，請參閱 W3C 簡易物件存取通訊協定 (SOAP) 1.1 中的 Soap 錯誤。  
  
### <a name="fault-code-information"></a>錯誤碼資訊  
 下表將顯示包含在 SOAP 回應之詳細資料區段中的 XMLA 錯誤碼資訊。 資料行是在 SOAP 錯誤的詳細資料區段中某個錯誤的屬性。  
  
|資料行名稱|類型|描述|允許的 null<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|傳回指出方法成功或失敗的代碼。 必須將十六進位值轉換成 `UnsignedInt` 值。|否|  
|`WarningCode`|`UnsignedInt`|傳回指出警告狀況的代碼。 必須將十六進位值轉換成 `UnsignedInt` 值。|是|  
|`Description`|`String`|產生錯誤的元件所傳回的警告文字與描述。|是|  
|`Source`|`String`|產生錯誤或警告之元件的名稱。|是|  
|`HelpFile`|`String`|描述錯誤或警告之說明檔或主題的路徑或 URL。|是|  
  
 <sup>1</sup>指出是否需要資料，且必須傳回，或是否資料是選擇性的如果不適用資料行允許 null 的字串。  
  
 下列是方法呼叫失敗時所發生的 SOAP 錯誤之範例：  
  
```  
<?xml version="1.0"?>  
   <SOAP-ENV:Envelope  
   xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
   SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
      <SOAP-ENV:Fault>  
         <faultcode>XMLAnalysisError.0x80000005</faultcode>  
         <faultstring>The XML for Analysis provider encountered an error.</faultstring>  
         <faultactor>XML for Analysis Provider</faultactor>  
         <detail>  
<Error  
ErrorCode="2147483653"  
Description="An unexpected error has occurred."  
Source="XML for Analysis Provider"  
HelpFile="" />  
         </detail>  
      </SOAP-ENV:Fault>  
</SOAP-ENV:Envelope>  
```  
  
##  <a name="handling_errors_and_warnings"></a> 處理錯誤和警告  
 如果下列情況在該命令執行之後發生，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會傳回 `Messages` 元素中的 `root` 屬性：  
  
-   方法本身並未失敗，但是方法呼叫成功之後，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上發生失敗。  
  
-   當命令成功時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會傳回警告。  
  
 `Messages` 屬性會遵循 `root` 元素所包含的所有其他屬性，而且可以包含一或多個 `Message` 元素。 因此，每個 `Message` 元素可包含單一 `error` 或 `warning` 元素，以分別描述指定命令所發生的任何錯誤或是警告。  
  
 如需有關錯誤和警告中所包含`Messages`屬性，請參閱 < [Messages 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)。  
  
### <a name="handling-errors-during-serialization"></a>處理序列化期間的錯誤。  
 如果發生錯誤之後[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體已經開始序列化成功執行的命令的輸出[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]會傳回[例外狀況](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla)錯誤不同命名空間中的項目。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體接著會關閉所有開啟的元素，這樣傳送到用戶端的 XML 文件就會是有效的文件。 執行個體也會傳回 `Messages` 元素，以包含錯誤的描述。  
  
##  <a name="handling_inline_errors_and_warnings"></a> 處理內嵌錯誤和警告  
 如果 XMLA 方法本身並未失敗，但是在 XMLA 方法呼叫成功之後，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上發生該方法傳回的結果中資料元素的特定錯誤，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為命令傳回內嵌 `error` 或 `warning`。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供內嵌`error`並`warning`項目，如果問題特定的儲存格，或其他資料，內含`root`項目使用[MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla)進行資料類型，例如安全性錯誤或格式化資料格的錯誤。 在這些情況下，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會傳回 `error` 或 `warning` 元素中，分別包含錯誤或警告的 `Cell` 或 `row` 元素。  
  
 下列範例說明結果集，其中包含從傳回的資料列集時發生`Execute`方法使用[陳述式](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令。  
  
```  
<return>  
   ...  
   <root>  
      ...  
      <CellData>  
      ...  
         <Cell CellOrdinal="10">  
            <Value>  
               <Error>  
                  <ErrorCode>2148497527</ErrorCode>   
                  <Description>Security Error.</Description>   
               </Error>  
            </Value>  
         </Cell>  
      </CellData>  
      ...  
   </root>  
   ...  
</return>  
```  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
