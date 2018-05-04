---
title: 處理錯誤和警告 (XMLA) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: de925e6bb83f7219ec1bd453f47d63a3fb3624a1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="handling-errors-and-warnings-xmla"></a>處理錯誤和警告 (XMLA)
  當 XML for Analysis (XMLA) 時，就需要錯誤處理[探索](../../analysis-services/xmla/xml-elements-methods-discover.md)或[Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫不會執行、 成功執行但產生錯誤或警告，或是成功執行但傳回的結果包含錯誤。  
  
|錯誤|報告|  
|-----------|---------------|  
|XMLA 方法呼叫未執行|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 傳回 SOAP 錯誤訊息包含失敗的詳細資料。<br /><br /> 如需詳細資訊，請參閱 > 一節，[處理 SOAP 錯誤](#handling_soap_faults)。|  
|方法呼叫成功時的錯誤或警告|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含[錯誤](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)或[警告](../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)項目，每個錯誤或警告，分別在[訊息](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)屬性[根](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)項目包含方法呼叫的結果。<br /><br /> 如需詳細資訊，請參閱 > 一節，[處理錯誤和警告](#handling_errors_and_warnings)。|  
|方法呼叫成功時結果中的錯誤|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含內嵌**錯誤**或**警告**項目錯誤或警告，分別內適當[儲存格](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)或[列](../../analysis-services/xmla/xml-elements-properties/row-element-xmla.md)方法呼叫的結果項目。<br /><br /> 如需詳細資訊，請參閱 > 一節，[處理內嵌錯誤和警告](#handling_inline_errors_and_warnings)。|  
  
##  <a name="handling_soap_faults"></a> 處理 SOAP 錯誤  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在發生下列情況時會傳回 SOAP 錯誤：  
  
-   包含 XMLA 方法的 SOAP 訊息，其格式不正確或是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體無法驗證它。  
  
-   發生通訊錯誤或是其他有關包含 XMLA 方法之 SOAP 訊息的錯誤。  
  
-   XMLA 方法並未在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上執行。  
  
 以 "XMLForAnalysis" 開頭的 XMLstartA 之 SOAP 錯誤碼，後面會接著句號和十六進位的 HRESULT 結果碼。 例如，`0x80000005` 的錯誤碼會格式化為 "`XMLForAnalysis.0x80000005`"。 如需有關 SOAP 錯誤格式的詳細資訊，請參閱 W3C 簡易物件存取通訊協定 (SOAP) 1.1 中的 Soap 錯誤。  
  
### <a name="fault-code-information"></a>錯誤碼資訊  
 下表將顯示包含在 SOAP 回應之詳細資料區段中的 XMLA 錯誤碼資訊。 資料行是在 SOAP 錯誤的詳細資料區段中某個錯誤的屬性。  
  
|資料行名稱|類型|Description|允許 null<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|**ErrorCode**|**UnsignedInt**|傳回指出方法成功或失敗的代碼。 十六進位值必須可轉換成**UnsignedInt**值。|否|  
|**WarningCode**|**UnsignedInt**|傳回指出警告狀況的代碼。 十六進位值必須可轉換成**UnsignedInt**值。|是|  
|**說明**|**字串**|產生錯誤的元件所傳回的警告文字與描述。|是|  
|**Source**|**字串**|產生錯誤或警告之元件的名稱。|是|  
|**HelpFile**|**字串**|描述錯誤或警告之說明檔或主題的路徑或 URL。|是|  
  
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
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 傳回**訊息**屬性**根**命令執行該命令之後，就會發生下列情況下，如果項目：  
  
-   方法本身並未失敗，但是方法呼叫成功之後，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上發生失敗。  
  
-   當命令成功時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會傳回警告。  
  
 **訊息**屬性會遵循所包含的其他所有屬性**根**項目，而且可以包含一或多個**訊息**項目。 接著，每個**訊息**項目可以包含單一**錯誤**或**警告**分別描述任何錯誤或警告，項目中發生的指定的命令。  
  
 如需詳細資訊，關於錯誤和警告中所包含的**訊息**屬性，請參閱[Messages 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)。  
  
### <a name="handling-errors-during-serialization"></a>處理序列化期間的錯誤。  
 如果發生錯誤之後[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體已經開始序列化成功執行的命令，輸出[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]傳回[例外狀況](../../analysis-services/xmla/xml-elements-properties/exception-element-xmla.md)錯誤不同命名空間中的項目。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體接著會關閉所有開啟的元素，這樣傳送到用戶端的 XML 文件就會是有效的文件。 執行個體也會傳回**訊息**包含錯誤的描述項目。  
  
##  <a name="handling_inline_errors_and_warnings"></a> 處理內嵌錯誤和警告  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 傳回內嵌**錯誤**或**警告**如果 XMLA 方法本身並未失敗，但發生錯誤之方法所傳回的結果中的資料元素的特定命令[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]XMLA 方法呼叫成功之後，執行個體。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供內嵌**錯誤**和**警告**項目有問題的特定資料格，或其他資料，內含**根**項目使用[MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)發生資料類型，例如安全性錯誤或資料格的格式錯誤。 在這些情況下，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]傳回**錯誤**或**警告**中的項目**儲存格**或**列**元素包含錯誤或警告，分別。  
  
 下列範例說明一個結果集，其中包含從傳回的資料列中的錯誤**Execute**方法使用[陳述式](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)命令。  
  
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
 [使用 Analysis Services 中的 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
