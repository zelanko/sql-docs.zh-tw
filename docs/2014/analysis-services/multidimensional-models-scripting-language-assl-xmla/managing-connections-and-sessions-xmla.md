---
title: 管理連接和會話（XMLA） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- statefulness [XML for Analysis]
- statelessness [XML for Analysis]
- XML for Analysis, sessions
- states [XML for Analysis]
- XMLA, sessions
- sessions [XML for Analysis]
ms.assetid: b83bb3ff-09be-4fda-9d1d-6248e04ffb21
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7bfe876f6874193fd0885f16d91caa9f6fe8b172
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544940"
---
# <a name="managing-connections-and-sessions-xmla"></a>管理連接與工作階段 (XMLA)
  *Statefulness*是伺服器在方法呼叫之間保留用戶端身分識別和內容的條件。 *Statelessness*是一種情況，在此情況中，伺服器不會在方法呼叫完成之後記住用戶端的身分識別和內容。  
  
 為了提供 statefulness，XML for Analysis （XMLA）支援允許一系列語句一起執行的*會話*。 這樣一系列的陳述式範例，將會建立用於後續查詢的導出成員。  
  
 一般而言，在 XMLA 中的工作階段會遵循 OLE DB 2.6 規格所述的下列行為：  
  
-   工作階段定義交易和命令內容範圍。  
  
-   在單一工作階段的內容中可以執行多個命令。  
  
-   XMLA 內容中的交易支援是透過與[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法一起傳送的提供者特定命令。  
  
 XMLA 定義了一個方法，可支援在 Web 環境中的工作階段，其所使用的模式類似於分散式撰寫及版本處理 (DAV) 通訊協定所使用的方法，可在鬆散偶合的環境中實作鎖定。 這個實作與 DAV 相似，因為其允許提供者基於各種理由 (例如，逾時或是連接錯誤) 使工作階段過期。 當再度支援工作階段時，Web 服務必須知道並準備處理必須重新啟動之中斷的命令集。  
  
 World Wide Web Consortium (W3C) 簡易物件存取通訊協定 (SOAP) 規格建議使用 SOAP 標頭，在 SOAP 訊息上面建立新的通訊協定。 下表列出 XMLA 為起始、維護和關閉工作階段，所定義的 SOAP 標頭元素與屬性。  
  
|SOAP 標頭|Description|  
|-----------------|-----------------|  
|BeginSession|此標頭要求提供者建立新的工作階段。 提供者應該建構新的工作階段，並在 SOAP 回應中，將工作階段識別碼與 Session 標頭一起傳回。|  
|SessionId|值區域包含的工作階段識別碼，必須用於工作階段其餘部分的每個方法呼叫。 在 SOAP 回應中的提供者會傳送這個標記，而用戶端也必須將這個屬性與每個 Session 標頭元素一起傳送。|  
|工作階段|對於每個發生在工作階段的方法呼叫，都必須使用這個標頭，而且在標頭的值區域中必須包括工作階段識別碼。|  
|EndSession|若要結束工作階段，請使用這個標頭。 值區域必須包括工作階段識別碼。|  
  
> [!NOTE]  
>  工作階段識別碼並不保證工作階段會維持有效狀態。 如果工作階段過期 (例如，如果逾時或是連接中斷)，提供者可以選擇結束和回復該工作階段的動作。 因此，所有後續從用戶端對工作階段識別碼發出的方法呼叫都會失敗，並產生指出工作階段無效的錯誤。 用戶端應該要處理這個狀況，並準備從頭開始，重新傳送工作階段方法呼叫。  
  
## <a name="legacy-code-example"></a>舊版程式碼範例  
 以下範例將示範如何支援工作階段。  
  
1.  若要開始工作階段，請將 SOAP 中的 BeginSession 標頭從用戶端加入輸出 XMLA 方法。 值區域一開始是空白的，因為還不知道工作階段識別碼。  
  
    ```  
    <SOAP-ENV:Envelope  
       xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
       SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
       <SOAP-ENV:Header>  
          <XA:BeginSession  
             xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
             xsi:type="xsd:int"  
             mustUnderstand="1"/>  
       </SOAP-ENV:Header>  
       <SOAP-ENV:Body>  
          ...<!-- Discover or Execute call goes here.-->  
       </SOAP-ENV:Body>  
    </SOAP-ENV:Envelope>  
    ```  
  
2.  來自提供者的 SOAP 回應訊息會使用 XMLA 標頭標記，將會話識別碼包含在傳回標頭區域中 \<SessionId> 。  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
3.  工作階段中的每個方法呼叫都必須加入 Session 標頭，以包含從提供者傳回的工作階段識別碼。  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
4.  當會話完成時， \<EndSession> 會使用標記，其中包含相關的會話識別碼值。  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:EndSession  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          xsi:type="xsd:int"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
