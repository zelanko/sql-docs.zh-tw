---
description: OpenSchema 方法
title: OpenSchema 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b0a92e7079338e290f228603767d6d15a3a351e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442920"
---
# <a name="openschema-method"></a>OpenSchema 方法
從提供者取得資料庫架構資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回包含架構資訊的 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件。 **記錄集會**以唯讀的靜態資料指標來開啟。 *QueryType*會決定哪些資料行出現在**記錄集中**。  
  
#### <a name="parameters"></a>參數  
 *QueryType*  
 代表要執行之架構查詢類型的任何 [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) 值。  
  
 *準則*  
 選擇性。 每個 *QueryType* 選項的查詢準則約束陣列，如 [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)中所列。  
  
 *SchemaID*  
 OLE DB 規格未定義之提供者架構查詢的 GUID。 如果 *QueryType* 設定為 **adSchemaProviderSpecific**，則需要這個參數;否則，就不會使用它。  
  
## <a name="remarks"></a>備註  
 **OpenSchema**方法會傳回資料來源的自我描述性資訊，例如資料來源中的資料表、資料表中的資料行，以及支援的資料類型。  
  
 *QueryType*引數是 GUID，表示) 傳回 (架構的資料行。 OLE DB 規格具有完整的架構清單。  
  
 *準則*引數會限制架構查詢的結果。 *準則* 指定的值陣列必須出現在產生的 **記錄集中**的對應資料行子集，稱為條件約束資料行。  
  
 如果提供者在先前所列的外部定義非標準的架構查詢，則會將常數 **adSchemaProviderSpecific** 用於 *QueryType* 引數。 使用這個常數時，必須要有 *SchemaID* 引數，才能傳遞要執行之架構查詢的 GUID。 如果 *QueryType* 設定為 **adSchemaProviderSpecific** ，但未提供 *SchemaID* ，則會產生錯誤。  
  
 提供者不需要支援所有的 OLE DB 標準架構查詢。 具體而言，OLE DB 規格只需要 **adSchemaTables**、 **adSchemaColumns**和 **adSchemaProviderTypes** 。 但是，提供者不需要支援先前針對這些架構查詢所列的 *準則條件* 約束。  
  
> [!NOTE]
>  **遠端資料服務使用量**用戶端[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件上無法使用**OpenSchema**方法。  
  
> [!NOTE]
>  在 Visual Basic 中，在**連接**物件上**OpenSchema**方法所傳回的**記錄集**內，具有四位元組不帶正負號的整數 (DBTYPE UI4) 的資料行，無法與其他變數進行比較。 如需 OLE DB 資料類型的詳細資訊，請參閱 [OLE DB (中的資料類型 OLE DB) ](https://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a) 和 [附錄 A：](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6) Microsoft OLE DB 程式設計人員參考中的資料類型。  
  
> [!NOTE]
>  **Visual C/c + + 使用者** 若未使用用戶端資料指標，則在 ADO 中抓取資料行架構的 "ORDINAL_POSITION"，會傳回 MDAC 2.7、MDAC 2.8 和 Windows Data Access 元件中類型 VT_R8 的 variant， (Windows DAC) 6.0，而 MDAC 2.6 中使用的類型則是 VT_I4。 針對 MDAC 2.6 所撰寫的程式，只要在 MDAC 2.7、MDAC 2.8 和 Windows DAC 6.0 下執行（不需要修改），就會針對每個序數取得零的 VT_I4。 進行這項變更的原因是，OLE DB 傳回的資料類型是 DBTYPE_UI4，而且在簽署的 VT_I4 中，沒有足夠的空間可包含所有可能的值，而且不可能發生截斷，因而導致資料遺失。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 OpenSchema 方法範例 ](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema 方法範例 (VC + +) ](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [ (ADO Connection) 的 Open 方法 ](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [ (ADO 記錄) 的 Open 方法 ](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [ (ADO 記錄集的 Open 方法) ](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [ (ADO Stream 的 Open 方法) ](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
