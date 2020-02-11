---
title: 建立新的外鍵範例（VC + +） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c812f0503b8801e861364a04e5621cb975adb009
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "76918072"
---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vc"></a>Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VC++)
下列程式碼示範如何建立新的外鍵。 它假設有兩個數據表（客戶和訂單）存在。  
  
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
      cout << "Error occurred in include files...." << endl;  
   }  
   ::CoUninitialize();  
}  
```
