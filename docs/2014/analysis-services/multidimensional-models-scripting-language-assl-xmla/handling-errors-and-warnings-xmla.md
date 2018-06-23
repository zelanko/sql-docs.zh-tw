---
title: 處理錯誤和警告 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5c59e6b0e5744fc118b23666a31f7300675ac115
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033136"
---
# <a name="handling-errors-and-warnings-xmla"></a>處理錯誤和警告 (XMLA)
  當 XML for Analysis (XMLA) 時，就需要錯誤處理[探索](../xmla/xml-elements-methods-discover.md)或[Execute](../xmla/xml-elements-methods-execute.md)方法呼叫不會執行、 成功執行但產生錯誤或警告，或是成功執行但傳回的結果包含錯誤。  
  
|錯誤|報告|  
|-----------|---------------|  
|XMLA 方法呼叫未執行|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 傳回 SOAP 錯誤訊息包含失敗的詳細資料。<br /><br /> 如需詳細資訊，請參閱 > 一節，[處理 SOAP 錯誤](#handling_soap_faults)。|  
|方法呼叫成功時的錯誤或警告|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含[錯誤](../xmla/xml-elements-properties/error-element-xmla.md)或[警告](../xmla/xml-elements-properties/warning-element-xmla.md)項目，每個錯誤或警告，分別在[訊息](../xmla/xml-elements-properties/messages-element-xmla.md)屬性[根](../xmla/xml-elements-properties/root-element-xmla.md)項目包含方法呼叫的結果。<br /><br /> 如需詳細資訊，請參閱 > 一節，[處理錯誤和警告](#handling_errors_and_warnings)。|  
|方法呼叫成功時結果中的錯誤|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含內嵌`error`或`warning`項目錯誤或警告，分別內適當[儲存格](../xmla/xml-elements-properties/cell-element-xmla.md)或[列](../xmla/xml-elements-properties/row-element-xmla.md)方法呼叫的結果中的項目。<br /><br /> 如需詳細資訊，請參閱 > 一節，[處理內嵌錯誤和警告](#handling_inline_errors_and_warnings)。|  
  
##  <a name="handling_soap_faults"></a> 處理 SOAP 錯誤  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在發生下列情況時會傳回 SOAP 錯誤：  
  
-   包含 XMLA 方法的 SOAP 訊息，其格式不正確或是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體無法驗證它。  
  
-   發生通訊錯誤或是其他有關包含 XMLA 方法之 SOAP 訊息的錯誤。  
  
-   XMLA 方法並未在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上執行。  
  
 以 "XMLForAnalysis" 開頭的 XMLstartA 之 SOAP 錯誤碼，後面會接著句號和十六進位的 HRESULT 結果碼。 例如，`0x80000005` 的錯誤碼會格式化為 "`XMLForAnalysis.0x80000005`"。 如需有關 SOAP 錯誤格式的詳細資訊，請參閱 W3C 簡易物件存取通訊協定 (SOAP) 1.1 中的 Soap 錯誤。  
  
### <a name="fault-code-information"></a>錯誤碼資訊  
 下表將顯示包含在 SOAP 回應之詳細資料區段中的 XMLA 錯誤碼資訊。 資料行是在 SOAP 錯誤的詳細資料區段中某個錯誤的屬性。  
  
|資料行名稱|類型|描述|允許 null<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|傳回指出方法成功或失敗的代碼。 必須將十六進位值轉換成 `UnsignedInt` 值。|否|  
|`WarningCode`|`UnsignedInt`|傳回指出警告狀況的代碼。 必須將十六進位值轉換成 `UnsignedInt` 值。|是|  
|`Description`|`String`|產生錯誤的元件所傳回的警告文字與描述。|是|  
|`Source`|`String`|產生錯誤或警告之元件的名稱。|是|  
|`HelpFile`|`String`|描述錯誤或警告之說明檔或主題的路徑或 URL。|是|  
  
 <sup>1</sup>資料需要和是否必須傳回，或是否是選擇性的資料，以及如果不適用資料行允許 null 的字串表示。  
  
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
  
 如需詳細資訊，關於錯誤和警告中所包含的`Messages`屬性，請參閱[Messages 元素&#40;XMLA&#41;](../xmla/xml-elements-properties/messages-element-xmla.md)。  
  
### <a name="handling-errors-during-serialization"></a>處理序列化期間的錯誤。  
 如果發生錯誤之後[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體已經開始序列化成功執行的命令，輸出[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]傳回[例外狀況](../xmla/xml-elements-properties/exception-element-xmla.md)錯誤不同命名空間中的項目。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體接著會關閉所有開啟的元素，這樣傳送到用戶端的 XML 文件就會是有效的文件。 執行個體也會傳回 `Messages` 元素，以包含錯誤的描述。  
  
##  <a name="handling_inline_errors_and_warnings"></a> 處理內嵌錯誤和警告  
 如果 XMLA 方法本身並未失敗，但是在 XMLA 方法呼叫成功之後，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上發生該方法傳回的結果中資料元素的特定錯誤，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為命令傳回內嵌 `error` 或 `warning`。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供內嵌`error`和`warning`項目有問題的特定資料格，或其他資料，內含`root`項目使用[MDDataSet](../xmla/xml-data-types/mddataset-data-type-xmla.md)發生資料類型，例如安全性錯誤，或格式設定資料格的錯誤。 在這些情況下，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會傳回 `error` 或 `warning` 元素中，分別包含錯誤或警告的 `Cell` 或 `row` 元素。  
  
 下列範例說明一個結果集，其中包含從傳回的資料列中的錯誤`Execute`方法使用[陳述式](../xmla/xml-elements-commands/statement-element-xmla.md)命令。  
  
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
  
  