---
title: PrimaryKey 和 Unique 屬性範例（VC + +） |Microsoft Docs
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
- Unique property [ADOX], VC++ example
- PrimaryKey property [ADOX], VC++ example
ms.assetid: d51814a2-ff7d-48ed-b719-99776da2091a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce3541843bc0eb82aa035864cd5c2490c4399ff5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "76918400"
---
# <a name="primarykey-and-unique-properties-example-vc"></a>PrimaryKey 和 Unique 屬性範例 (VC++)
這個範例示範[索引](../../../ado/reference/adox-api/index-object-adox.md)的[PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md)和[Unique](../../../ado/reference/adox-api/unique-property-adox.md)屬性。 此程式碼會建立包含兩個數據行的新資料表。 **PrimaryKey**和**Unique**屬性是用來將一個資料行設為不允許重複值的主要索引鍵。  
  
```  
// BeginPrimaryKeyCpp.cpp  
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
   _TablePtr m_pTableNew = NULL;  
   _IndexPtr m_pIndexNew  = NULL;  
   _IndexPtr m_pIndex  = NULL;  
   _ColumnPtr m_pColumn = NULL;  
  
   // Define string variable  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data Source = 'c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
      TESTHR(hr = m_pTableNew.CreateInstance(__uuidof(Table)));  
      TESTHR(hr = m_pIndexNew.CreateInstance(__uuidof(Index)));  
      TESTHR(hr = m_pIndex.CreateInstance(__uuidof(Index)));  
      TESTHR(hr = m_pColumn.CreateInstance(__uuidof(Column)));  
  
      // Connect the catalog  
      m_pCatalog->PutActiveConnection(strcnn);  
  
      // Name new table  
      m_pTableNew->Name = "NewTable";  
  
      // Append a numeric and a text field to new table.  
      m_pTableNew->Columns->Append("NumField", adInteger, 20);  
      m_pTableNew->Columns->Append("TextField", adVarWChar, 20);  
  
      // Append new Primary Key index on NumField column to new table  
      m_pIndexNew->Name = "NumIndex";  
      m_pIndexNew->Columns->Append("NumField", adInteger, 0);  
      // here "-1" is required instead of "true".  
      m_pIndexNew->PutPrimaryKey(-1);  
      m_pIndexNew->PutUnique(-1);  
      m_pTableNew->Indexes->Append(_variant_t ((IDispatch*)m_pIndexNew));  
  
      // Append an index on Textfield to new table.  Note the different technique: Specifying   
      // index and column name as parameters of the Append method  
      m_pTableNew->Indexes->Append("TextIndex", "TextField");  
  
      // Append the new table  
      m_pCatalog->Tables->Append(_variant_t ((IDispatch*)m_pTableNew));  
  
      cout << m_pTableNew->Indexes->Count << " Indexes in " << m_pTableNew->Name << " Table" << endl;  
      m_pCatalog->Tables->Refresh();  
  
      _variant_t vIndex;  
      // Enumerate Indexes collection.  
      for ( long lIndex = 0 ; lIndex < m_pTableNew->Indexes->Count ; lIndex++ ) {  
         vIndex = lIndex;  
         m_pIndex = m_pTableNew->Indexes->GetItem(vIndex);  
         cout << "Index " << m_pIndex->Name << endl;  
         cout << "   Primary key = " << (m_pIndex->GetPrimaryKey() ? "True" : "False") << endl;  
         cout << "   Unique = "  << (m_pIndex->GetUnique() ? "True" : "False") << endl;  
  
         // Enumerate Columns collection of each Index object.  
         cout << "    Columns" << endl;  
  
         for ( long lIndex = 0 ; lIndex < m_pIndex->Columns->Count ; lIndex++ ) {  
            vIndex = lIndex;  
            m_pColumn = m_pIndex->Columns->GetItem(vIndex);  
            cout << "       " << m_pColumn->Name << endl;  
         }  
      }  
  
      // Delete new table as this is a demonstration  
      m_pCatalog->Tables->Delete(m_pTableNew->Name);  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occurred in PrimaryKeyX...." << endl;  
   }  
  
   m_pCatalog = NULL;  
   ::CoUninitialize();  
}  
```
