---
description: Column 物件的 NumericScale 和 Precision 屬性範例 (VC++)
title: " (VC + +) 的資料行範例的 NumericScale 和精確度屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Precision property [ADOX], VC++ example
- NumericScale property [ADOX], VC++ example
ms.assetid: 69653366-ebd7-4ff6-a654-761772223b0c
author: rothja
ms.author: jroth
ms.openlocfilehash: 9b7ca5a849dafe9768a422a942f5c2c1816f77b1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983899"
---
# <a name="numericscale-and-precision-properties-of-the-column-object-example-vc"></a>Column 物件的 NumericScale 和 Precision 屬性範例 (VC++)
此範例示範資料[行](./column-object-adox.md)物件的[NumericScale](./numericscale-property-adox.md)和[Precision](./precision-property-adox.md)屬性。 此程式碼會顯示*Northwind*資料庫之 [**訂單詳細資料**] 資料表的值。  
  
```  
// BeginNumericScalePrecCpp.cpp  
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
  
   // Define and initialize ADOX object pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
   _ColumnPtr m_pColumn = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
  
   // Declare string variables  
   _bstr_t strCnn("Provider='Microsoft.JET.OLEDB.4.0';Data Source='c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
  
      // Connect the catalog.  
      m_pCnn->Open (strCnn, "", "", NULL);  
  
      m_pCatalog->PutActiveConnection(variant_t((IDispatch *)m_pCnn));  
  
      // Retrieve the Order Details table  
      m_pTable = m_pCatalog->Tables->GetItem("Order Details");  
  
      // Display numeric scale and precision of small integer fields.  
      _variant_t vIndex;  
      for ( long lIndex = 0 ; lIndex < m_pTable->Columns->Count ; lIndex++ ) {  
         vIndex = lIndex ;  
         m_pColumn = m_pTable->Columns->GetItem(vIndex);  
         if (m_pColumn->Type == adSmallInt) {  
            cout << "Column: " << m_pColumn->GetName() << endl;  
            cout << "Numeric scale: " << (_bstr_t) m_pColumn->GetNumericScale() << endl;  
            cout << "Precision: " << m_pColumn->GetPrecision() << endl;  
         }  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occurred in NumericScalePrecX...." << endl;  
   }  
   ::CoUninitialize();  
}  
```