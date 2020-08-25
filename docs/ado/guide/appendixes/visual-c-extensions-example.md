---
description: Visual C++ Extensions 範例
title: Visual C++ 擴充功能範例 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions example
ms.assetid: 9739c278-582c-402b-a158-7f68a1b2c293
author: rothja
ms.author: jroth
ms.openlocfilehash: ae7eaab32f14ce653d766cfe38408118cc37b763
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806781"
---
# <a name="visual-c-extensions-example"></a>Visual C++ Extensions 範例
此程式會顯示如何從欄位取出值，並轉換成 C/c + + 變數。  
  
 這個範例也會利用「智慧型指標」，這會自動處理 `QueryInterface` **IADORecordBinding** 介面之呼叫和參考計數的 COM 特定詳細資料。  
  
 如果沒有智慧型指標，您可以撰寫程式碼：  
  
```cpp
IADORecordBinding   *picRs = NULL;  
...  
TESTHR(pRs->QueryInterface(  
          __uuidof(IADORecordBinding), (LPVOID*)&picRs));  
...  
if (picRs) picRs->Release();  
```  
  
 使用智慧型指標，您可以 `IADORecordBindingPtr` 使用下列語句從介面衍生型別 `IADORecordBinding` ：  
  
```cpp
_COM_SMARTPTR_TYPEDEF(IADORecordBinding, __uuidof(IADORecordBinding));  
```  
  
 然後具現化指標，如下所示：  
  
```cpp
IADORecordBindingPtr picRs(pRs);  
```  
  
 由於 Visual C++ 延伸模組是由 **記錄集** 物件所執行，因此智慧型指標的函式 `picRs` 會採用 _ `RecordsetPtr` 指標 `pRs` 。 使用的函式會呼叫 `QueryInterface` `pRs` ，以找出 `IADORecordBinding` 介面。  
  
```cpp
// Visual_Cpp_Extensions_Example.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <icrsint.h>  
_COM_SMARTPTR_TYPEDEF(IADORecordBinding, __uuidof(IADORecordBinding));  
  
inline void TESTHR(HRESULT _hr) { if FAILED(_hr) _com_issue_error(_hr); }  
  
class CCustomRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CCustomRs)  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_ch_fname, sizeof(m_ch_fname), m_ul_fnameStatus, false)  
      ADO_VARIABLE_LENGTH_ENTRY2(4, adVarChar, m_ch_lname, sizeof(m_ch_lname), m_ul_lnameStatus, false)  
   END_ADO_BINDING()  
  
public:  
   CHAR m_ch_fname[22];  
   CHAR m_ch_lname[32];  
   ULONG m_ul_fnameStatus;  
   ULONG m_ul_lnameStatus;  
};  
  
int main() {  
   ::CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      CCustomRs rs;  
      IADORecordBindingPtr picRs(pRs);  
  
      pRs->Open(L"SELECT * FROM Employee ORDER BY lname", L"dsn=DataPubs;Trusted_Connection=yes;", adOpenStatic, adLockOptimistic, adCmdText);  
  
      TESTHR(picRs->BindToRecordset(&rs));  
  
      while (!pRs->EndOfFile) {  
         // Process data in the CCustomRs C++ instance variables.  
         printf("Name = %s %s\n",  
            (rs.m_ul_fnameStatus == adFldOK ? rs.m_ch_fname: "<Error>"),   
            (rs.m_ul_lnameStatus == adFldOK ? rs.m_ch_lname: "<Error>") );  
  
         // Move to the next row of the Recordset.   Fields in the new row will   
         // automatically be placed in the CCustomRs C++ instance variables.  
  
         pRs->MoveNext();  
      }  
   }  
   catch (_com_error &e ) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Meaning = %s\n", e.ErrorMessage());  
      printf("Source = %s\n", (LPCSTR) e.Source());  
      printf("Description = %s\n", (LPCSTR) e.Description());  
   }  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 Visual C++ 擴充功能](./using-visual-c-extensions.md)   
 [Visual C++ Extensions 標題](./visual-c-extensions-header.md)