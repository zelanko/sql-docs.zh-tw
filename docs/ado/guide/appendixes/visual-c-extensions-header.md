---
title: Visual C++ 延伸模組標頭 |Microsoft Docs
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
- Visual C++ [ADO]
ms.assetid: e492d307-24cb-489c-a5b0-99cdc09b07da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 675a31ab333a6c2d92e6afcd6a461b3baebd5b3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926381"
---
# <a name="visual-c-extensions-header"></a>Visual C++ Extensions 標題
下列標頭**icrsint**詳述的介面，可讓用戶端將**記錄集**的欄位，抓取至衍生自**CADORecordBinding**的類別中所定義的變數。 您必須為您想要存取的每個欄位指定 ADO 系結宏。  
  
```cpp
#ifndef _ICRSINT_H_  
#define _ICRSINT_H_  
  
#include <olectl.h>  
#include <stddef.h>  
  
// forwards  
class CADORecordBinding;  
  
#define classoffset(base, derived) ((DWORD)(static_cast<base*>((derived*)8))-8)  
  
enum ADOFieldStatusEnum  
{     
   adFldOK = 0,  
   adFldBadAccessor = 1,  
   adFldCantConvertValue = 2,  
   adFldNull = 3,  
   adFldTruncated = 4,  
   adFldSignMismatch = 5,  
   adFldDataOverFlow = 6,  
   adFldCantCreate = 7,  
   adFldUnavailable = 8,  
   adFldPermissionDenied = 9,  
   adFldIntegrityViolation = 10,  
   adFldSchemaViolation = 11,  
   adFldBadStatus = 12,  
   adFldDefault = 13  
};  
  
typedef struct stADO_BINDING_ENTRY  
{  
   ULONG      ulOrdinal;  
   WORD       wDataType;  
   BYTE       bPrecision;  
   BYTE       bScale;  
   ULONG      ulSize;  
   ULONG      ulBufferOffset;  
   ULONG      ulStatusOffset;  
   ULONG      ulLengthOffset;  
   ULONG      ulADORecordBindingOffSet;  
   BOOL       fModify;  
} ADO_BINDING_ENTRY;  
  
#define BEGIN_ADO_BINDING(cls) public: \  
   typedef cls ADORowClass; \  
   const ADO_BINDING_ENTRY* STDMETHODCALLTYPE GetADOBindingEntries() { \  
   static const ADO_BINDING_ENTRY rgADOBindingEntries[] = {   
  
//  
// Fixed length non-numeric data  
//  
#define ADO_FIXED_LENGTH_ENTRY(Ordinal, DataType, Buffer, Status, Modify)\  
   {Ordinal, \  
   DataType, \  
   0, \  
   0, \  
   0, \  
   offsetof(ADORowClass, Buffer), \  
   offsetof(ADORowClass, Status), \  
   0, \  
   classoffset(CADORecordBinding, ADORowClass), \  
   Modify},  
  
#define ADO_FIXED_LENGTH_ENTRY2(Ordinal, DataType, Buffer, Modify)\  
   {Ordinal, \  
   DataType, \  
   0, \  
   0, \  
   0, \  
   offsetof(ADORowClass, Buffer), \  
   0, \  
   0, \  
   classoffset(CADORecordBinding, ADORowClass), \  
   Modify},  
  
//  
// Numeric data  
//   
#define ADO_NUMERIC_ENTRY(Ordinal, DataType, Buffer, Precision, Scale, Status, Modify)\  
   {Ordinal, \  
   DataType, \  
   Precision, \  
   Scale, \  
   0, \  
   offsetof(ADORowClass, Buffer), \  
   offsetof(ADORowClass, Status), \  
   0, \  
   classoffset(CADORecordBinding, ADORowClass), \  
   Modify},  
  
#define ADO_NUMERIC_ENTRY2(Ordinal, DataType, Buffer, Precision, Scale, Modify)\  
   {Ordinal, \  
   DataType, \  
   Precision, \  
   Scale, \  
   0, \  
   offsetof(ADORowClass, Buffer), \  
   0, \  
   0, \  
   classoffset(CADORecordBinding, ADORowClass), \  
   Modify},  
  
//  
// Variable length data  
//  
#define ADO_VARIABLE_LENGTH_ENTRY(Ordinal, DataType, Buffer, Size, Status, Length, Modify)\  
   {Ordinal, \  
   DataType, \  
   0, \  
   0, \  
   Size, \  
   offsetof(ADORowClass, Buffer), \  
   offsetof(ADORowClass, Status), \  
   offsetof(ADORowClass, Length), \  
   classoffset(CADORecordBinding, ADORowClass), \  
   Modify},  
  
#define ADO_VARIABLE_LENGTH_ENTRY2(Ordinal, DataType, Buffer, Size, Status, Modify)\  
   {Ordinal, \  
   DataType, \  
   0, \  
   0, \  
   Size, \  
   offsetof(ADORowClass, Buffer), \  
   offsetof(ADORowClass, Status), \  
   0, \  
   classoffset(CADORecordBinding, ADORowClass), \  
   Modify},  
  
#define ADO_VARIABLE_LENGTH_ENTRY3(Ordinal, DataType, Buffer, Size, Length, Modify)\  
   {Ordinal, \  
   DataType, \  
   0, \  
   0, \  
   Size, \  
   offsetof(ADORowClass, Buffer), \  
   0, \  
   offsetof(ADORowClass, Length), \  
   classoffset(CADORecordBinding, ADORowClass), \  
   Modify},  
  
#define ADO_VARIABLE_LENGTH_ENTRY4(Ordinal, DataType, Buffer, Size, Modify)\  
   {Ordinal, \  
   DataType, \  
   0, \  
   0, \  
   Size, \  
   offsetof(ADORowClass, Buffer), \  
   0, \  
   0, \  
   classoffset(CADORecordBinding, ADORowClass), \  
   Modify},  
  
#define END_ADO_BINDING()   {0, adEmpty, 0, 0, 0, 0, 0, 0, 0, FALSE}};\  
   return rgADOBindingEntries;}  
  
//  
// Interface that the client 'record' class needs to support. The ADO Binding entries  
// provide the implementation for this interface.  
//  
class CADORecordBinding  
{  
public:  
   STDMETHOD_(const ADO_BINDING_ENTRY*, GetADOBindingEntries) (VOID) PURE;  
};  
  
//  
// Interface that allows a client to fetch a record of data into class data members.  
//  
struct __declspec(uuid("00000544-0000-0010-8000-00aa006d2ea4")) IADORecordBinding;  
DECLARE_INTERFACE_(IADORecordBinding, IUnknown)  
{  
public:  
   STDMETHOD(BindToRecordset) (CADORecordBinding *pAdoRecordBinding) PURE;  
   STDMETHOD(AddNew) (CADORecordBinding *pAdoRecordBinding) PURE;  
   STDMETHOD(Update) (CADORecordBinding *pAdoRecordBinding) PURE;  
};  
  
#endif // !_ICRSINT_H_  
```  
  
## <a name="see-also"></a>另請參閱  
 [Visual C++ 延伸模組範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)   
 [使用 Visual C++ Extensions](../../../ado/guide/appendixes/using-visual-c-extensions.md)
