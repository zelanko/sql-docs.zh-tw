---
title: 建立方法的範例 （VC + +） |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Create method [ADOX], VC++ example
ms.assetid: 57fcb0eb-5d40-4ad4-996d-380732de8a3d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87bc653b51b8f1e0c0c98d05a02f93a814bb7706
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="create-method-example-vc"></a>建立方法的範例 （VC + +）
下列程式碼示範如何建立新的 Microsoft Jet 資料庫與[建立](../../../ado/reference/adox-api/create-method-adox.md)方法。  
  
```  
// BeginCreateDatabaseCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#define TESTHR(x) if FAILED(x) _com_issue_error(x);  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
void CreateDatabaseX(void);  
  
int main() {  
   HRESULT hr = S_OK;  
  
   hr = ::CoInitialize(NULL);  
   if (SUCCEEDED(hr)) {  
      CreateDatabaseX();  
      ::CoUninitialize();  
   }  
}  
  
// Create a new Jet database with the Create method  
void CreateDatabaseX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
  
   // Set ActiveConnection of Catalog to this string  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = c:\\new.mdb");  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      m_pCatalog->Create(strcnn);  
      printf("Database 'c:\\new.mdb' is created.\n");  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in CreateDatabaseX...." << endl;  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [Create 方法 (ADOX)](../../../ado/reference/adox-api/create-method-adox.md)
