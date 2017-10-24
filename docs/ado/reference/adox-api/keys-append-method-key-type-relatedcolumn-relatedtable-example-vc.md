---
title: "建立新的外部索引鍵範例 （VC + +） |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- RelatedTable property [ADOX], VC++ example
- Key Type property [ADOX], VC++ example
- UpdateRule property [ADOX], VC++ example
- Append method [ADOX], VC++ example
- Keys Append method [ADOX], VC++ example
- RelatedColumn property [ADOX], VC++ example
ms.assetid: 28495b8f-18dc-482c-995d-a120f6ae2006
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8b435b9550c2d18248797bc88ee68eb3e0a1ddff
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vc"></a>索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 （VC + +）
下列程式碼會示範如何建立新的外部索引鍵。 它會假設有兩個資料表 （客戶和訂單）。  
  
```  
// BeginCreateKeyCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )   
      return -1;  
  
   HRESULT hr = S_OK;  
  
   // Define and initialize ADOX object pointers.  These are in ADODB namespace.  
   _KeyPtr m_pKeyForeign = NULL;   
   _CatalogPtr m_pCatalog = NULL;  
  
   // Define other variables  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = 'c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pKeyForeign.CreateInstance(__uuidof(Key)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      m_pCatalog->PutActiveConnection(strcnn);  
  
      // Define the foreign key.  
      m_pKeyForeign->Name = "CustOrder";  
      m_pKeyForeign->Type = adKeyForeign;  
      m_pKeyForeign->RelatedTable = "Customers";  
      m_pKeyForeign->Columns->Append("CustomerId",adVarWChar,0);  
      m_pKeyForeign->Columns->GetItem("CustomerId")->RelatedColumn = "CustomerId";  
      m_pKeyForeign->UpdateRule = adRICascade;  
  
      // To pass as column parameter to Key's Apppend method  
      _variant_t vOptional;  
      vOptional.vt = VT_ERROR;  
      vOptional.scode = DISP_E_PARAMNOTFOUND;  
  
      // Append the foreign key.  
      m_pCatalog->Tables->GetItem("Orders")->Keys->Append(_variant_t((IDispatch *)m_pKeyForeign),  
         adKeyPrimary,  
         vOptional,  
         L"",  
         L"");  
      printf("Foreign key 'CustOrder' is added.\n");  
  
      // Delete the key as this is a demonstration.  
      m_pCatalog->Tables->GetItem("Orders")->Keys->Delete(m_pKeyForeign->Name);  
      printf("Foreign key 'CustOrder' is deleted.\n");  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
  
   catch(...) {  
      cout << "Error occured in include files...." << endl;  
   }  
   ::CoUninitialize();  
}  
```

