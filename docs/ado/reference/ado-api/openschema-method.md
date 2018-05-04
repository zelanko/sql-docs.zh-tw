---
title: OpenSchema 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52eaf3a58ae7f6eeaddecb943b5a129dec5e44e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="openschema-method"></a>OpenSchema 方法
從提供者取得資料庫結構描述資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，其中包含結構描述資訊。 **資料錄集**會開啟為唯讀、 靜態資料指標。 *QueryType*決定資料行出現在**資料錄集**。  
  
#### <a name="parameters"></a>參數  
 *QueryType*  
 任何[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)值，表示結構描述執行的查詢類型。  
  
 *準則*  
 選擇性。 陣列的每個查詢條件約束*QueryType*選項，如下所示[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)。  
  
 *SchemaID*  
 提供者結構描述查詢不是 OLE DB 規格所定義的 GUID。 這個參數是必要項，如果*QueryType*設為**adSchemaProviderSpecific**，否則不會使用它。  
  
## <a name="remarks"></a>備註  
 **OpenSchema**方法會傳回有關資料來源，例如資料表是資料來源，在資料表中的資料行中的自我描述資訊和支援的資料類型。  
  
 *QueryType*引數是指示傳回資料行 （結構描述） 的 GUID。 OLE DB 規格具有結構描述的完整清單。  
  
 *準則*引數會限制結構描述查詢的結果。 *準則*指定必須發生的值陣列中對應資料行，稱為條件約束的資料行，在產生的子集**資料錄集**。  
  
 常數**adSchemaProviderSpecific**用於*QueryType*引數如果提供者會定義它自己的非標準的結構描述查詢之外的先前所列。 使用這個常數時， *SchemaID*引數，才能傳遞要執行的結構描述查詢的 GUID。 如果*QueryType*設**adSchemaProviderSpecific**但*SchemaID*未提供，會導致錯誤。  
  
 提供者不支援所需的所有 OLE DB 標準的結構描述查詢。 具體來說，只有**adSchemaTables**， **adSchemaColumns**，和**adSchemaProviderTypes**所需的 OLE DB 規格。 不過，提供者不需要支援*準則*條件約束稍早所列的這些查詢的結構描述。  
  
> [!NOTE]
>  **遠端資料服務使用量** **OpenSchema**方法並不適用於用戶端[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
> [!NOTE]
>  在 Visual Basic 中，有四個位元組不帶正負號的整數 (DBTYPE UI4) 中的資料行**資料錄集**從傳回**OpenSchema**方法**連接**物件無法其他變數進行比較。 如需有關 OLE DB 資料類型的詳細資訊，請參閱[OLE DB (OLE DB) 中的資料型別](http://msdn.microsoft.com/en-us/6039292f-74e0-49b2-b133-17bc117ebf6a)和[附錄 a： 資料型別](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6)Microsoft OLE DB 程式設計人員參考中。  
  
> [!NOTE]
>  **Visual C/c + + 使用者**時不使用用戶端資料指標，擷取資料行中的結構描述 ADO"ORDINAL_POSITION"傳回類型 VT_R8 MDAC 2.7、 MDAC 2.8 和 Windows Data Access Components (Windows DAC) 6.0，同時使用 MDAC 中的類型中的 variant2.6 為 VT_I4。 撰寫的 MDAC 2.6 變化，讓只有尋找程式傳回的類型 VT_I4 得到為零，如果必須修改才能執行 MDAC 2.7、 MDAC 2.8 與 Windows DAC 6.0 下每個序數。 因為傳回 OLE DB 資料類型為 DBTYPE_UI4，進行這項變更，並帶正負號的 VT_I4 類型中沒有足夠的空間，以包含所有可能的值，而不可能被截斷發生，因而導致資料遺失。  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [OpenSchema 方法範例 (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema 方法範例 （VC + +）](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open 方法 （ADO 連接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 資料錄）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 （ADO 資料流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
